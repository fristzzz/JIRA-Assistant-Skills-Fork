# Quick Start: 5-Minute Patterns

Get up and running with bulk operations in under 5 minutes.

---

## Choose Your Path

### I have 5-10 issues to update

Use preview-first execution even for smaller batches:

```bash
# Transition issues (preview)
jira-as bulk transition --issues PROJ-1,PROJ-2,PROJ-3 --to Done --dry-run

# Transition issues (execute after review)
jira-as bulk transition --issues PROJ-1,PROJ-2,PROJ-3 --to Done

# Assign issues
jira-as bulk assign --issues PROJ-1,PROJ-2 --assignee john.doe --dry-run
jira-as bulk assign --issues PROJ-1,PROJ-2 --assignee john.doe

# Set priority
jira-as bulk set-priority --issues PROJ-1,PROJ-2 --priority High --dry-run
jira-as bulk set-priority --issues PROJ-1,PROJ-2 --priority High

# Clone issues
jira-as bulk clone --issues PROJ-1,PROJ-2 --include-subtasks --dry-run
jira-as bulk clone --issues PROJ-1,PROJ-2 --include-subtasks
```

---

### I have 50-100 issues to update

Use dry-run first to preview changes:

```bash
# Step 1: Preview what will happen
jira-as bulk transition --jql "project=PROJ AND status='In Progress'" --to Done --dry-run

# Step 2: Review output - verify count and sample issues

# Step 3: Execute
jira-as bulk transition --jql "project=PROJ AND status='In Progress'" --to Done
```

**Tip:** Operations over 50 issues will prompt for confirmation. Use `--yes` to skip (with caution).

---

### I have 500+ issues to update

Use dry-run first, then execute in bounded batches:

```bash
# Step 1: Preview
jira-as bulk transition --jql "project=PROJ" --to Done --dry-run

# Step 2: Execute first batch
jira-as bulk transition \
  --jql "project=PROJ AND key >= PROJ-1 AND key <= PROJ-200" \
  --to Done

# Step 3: Execute next batches with adjusted JQL ranges
```

---

## Essential Options

| Option | When to Use | Example |
|--------|-------------|---------|
| `--dry-run` | Preview changes (>10 issues) | `--dry-run` |
| `--max-issues N` | Limit scope for testing | `--max-issues 100` |
| `--yes` | Skip confirmation in automation | `--yes` |

---

## Common Scenarios

### Sprint Cleanup

```bash
# Close all done items from current sprint
jira-as bulk transition \
  --jql "sprint in openSprints() AND status='Verified'" \
  --to Done \
  --resolution Done \
  --dry-run
```

### Team Member Reassignment

```bash
# Reassign open work from leaving team member
jira-as bulk assign \
  --jql "assignee=john.leaving AND status NOT IN (Done, Closed)" \
  --assignee jane.replacing \
  --dry-run
```

### Priority Escalation

```bash
# Bump all critical bugs to Highest priority
jira-as bulk set-priority \
  --jql "type=Bug AND labels=critical AND priority != Highest" \
  --priority Highest \
  --dry-run
```

### Sprint Cloning

```bash
# Clone entire sprint to new project
jira-as bulk clone \
  --jql "sprint='Sprint 42'" \
  --target-project NEWPROJ \
  --include-subtasks \
  --include-links \
  --prefix "[Clone]" \
  --dry-run
```

---

## Next Steps

- **Which command should I use?** See [Operations Guide](OPERATIONS_GUIDE.md)
- **How should I split large runs?** Use JQL ranges plus `--max-issues`
- **Something went wrong?** See [Error Recovery](ERROR_RECOVERY.md)
- **Planning a big operation?** See [Best Practices](BEST_PRACTICES.md)
