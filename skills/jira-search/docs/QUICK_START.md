# JIRA Search Quick Start

Get started with JQL search in 5 minutes.

---

## Your First Search

### Step 1: Verify Setup

```bash
# Test connectivity with a simple search
jira-as search query "project = PROJ" --max-results 1
```

If this works, you are ready to search.

### Step 2: Find Your Issues

```bash
# Find all issues assigned to you
jira-as search query "assignee = currentUser() AND status != Done"
```

### Step 3: Search by Criteria

```bash
# Find open bugs in a project
jira-as search query "project = PROJ AND type = Bug AND status = Open"

# Find high priority work
jira-as search query "priority IN (Highest, High) AND status != Done"

# Find issues created this week
jira-as search query "created >= startOfWeek()"
```

---

## Common Search Patterns

| Goal | JQL Query | Command |
|------|-----------|---------|
| My work | `assignee = currentUser() AND status != Done` | `jira-as search query "..."` |
| Team bugs | `assignee IN membersOf("team") AND type = Bug` | `jira-as search query "..."` |
| Overdue | `duedate < now() AND status != Done` | `jira-as search query "..."` |
| Created today | `created >= startOfDay()` | `jira-as search query "..."` |
| Unassigned | `assignee IS EMPTY AND status = Open` | `jira-as search query "..."` |

---

## 5 Most Common Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `jira-as search query` | Execute JQL queries | `jira-as search query "project = PROJ"` |
| `jira-as search export` | Export to CSV/JSON | `jira-as search export "project = PROJ" -o report.csv` |
| `jira-as search filter create` | Save a reusable filter | `jira-as search filter create -n "My Filter" -j "assignee = currentUser()"` |
| `jira-as search validate` | Check JQL syntax | `jira-as search validate "your query"` |
| `jira-as search filter run` | Run a saved filter | `jira-as search filter run --name "Sprint Issues"` |

---

## Quick Troubleshooting

**"No issues found"**
```bash
# Validate your query syntax
jira-as search validate "your query here"
```

**"401 Unauthorized"**
- Check your API token at https://id.atlassian.com/manage-profile/security/api-tokens
- Verify `JIRA_EMAIL` matches your token's email

**"Field not found"**
```bash
# List available fields
jira-as search fields --filter fieldname
```

**"Query too slow"**
- Add `project = PROJ` to limit scope
- Use `--fields key,summary,status` to limit returned data

---

## Next Steps

### Learn JQL Syntax
- See [references/jql_reference.md](../references/jql_reference.md) for operators and functions
- See [references/search_examples.md](../references/search_examples.md) for query patterns

### Save and Share Searches
1. Create a filter: `jira-as search filter create -n "Filter Name" -j "JQL query" -f`
2. Share with team: `jira-as search filter share FILTER_ID --project PROJ`
3. Run later: `jira-as search filter run --name "Filter Name"`

### Export Data
- Small exports: `jira-as search export "query" -o report.csv`
- Large exports (>5000): `jira-as search export "query" -o report.csv --fields key,summary,status`

### Build Complex Queries
```bash
# Get field suggestions
jira-as search suggest --field status

# Build query from clauses
jira-as search build --clause "project = PROJ" --clause "status = Open" --validate
```

---

## Quick Reference

```bash
# Essential commands
jira-as search query "JQL"              # Search
jira-as search validate "JQL"           # Validate
jira-as search export "JQL" -o FILE     # Export
jira-as search filter create -n NAME -j "JQL"  # Save filter
jira-as search filter run --name NAME   # Run filter
```

For complete documentation, see:
- [SKILL.md](../SKILL.md) - Full capabilities overview
- [SCRIPT_REFERENCE.md](SCRIPT_REFERENCE.md) - Full command mapping and examples
- [references/BEST_PRACTICES.md](../references/BEST_PRACTICES.md) - Expert guide
