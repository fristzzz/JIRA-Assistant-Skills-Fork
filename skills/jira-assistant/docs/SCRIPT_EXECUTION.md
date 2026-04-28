# CLI Execution Guidelines

**IMPORTANT: Always verify command syntax before execution.**

Before running any JIRA command, check syntax and available options:

```bash
# Always run --help first to verify syntax
jira-as <area> <command> --help
```

---

## Why This Matters

1. **Parameter validation** - Confirm required vs optional arguments
2. **Correct flags** - Verify exact flag names (e.g., `--issue-key` vs `--issue`)
3. **Value formats** - Check expected formats (dates, time strings, JQL)
4. **Avoid failures** - Prevent execution errors from incorrect syntax

---

## Execution Pattern

Follow this pattern for every CLI operation:

```bash
# Step 1: Check syntax first
jira-as issue create --help

# Step 2: Execute with verified parameters
jira-as issue create --project PROJ --type Bug --summary "Issue title"
```

---

## Common Parameter Patterns

| Pattern | Example | Notes |
|---------|---------|-------|
| Issue key | `PROJ-123` | Positional or `--issue-key` |
| Project | `--project PROJ` | 2-10 char uppercase |
| Profile | `--profile development` | JIRA instance to use |
| Dry run | `--dry-run` | Preview without changes |
| Output | `--output json` | json, table, or csv |

---

## Error Prevention

When a command fails:
1. Re-run with `--help` to verify exact syntax
2. Check if required parameters are missing
3. Validate parameter value formats
4. Verify `--profile` matches configured instance

---

## Command Groups by Skill

| Skill | Command Group | Common Commands |
|-------|---------------|-----------------|
| jira-issue | `jira-as issue` | `create`, `get`, `update`, `delete` |
| jira-lifecycle | `jira-as lifecycle` | `transition`, `assign`, `version`, `component` |
| jira-search | `jira-as search` | `query`, `validate`, `build`, `export` |
| jira-collaborate | `jira-as collaborate` | `comment`, `attachment`, `notify`, `watchers` |
| jira-agile | `jira-as agile` | `epic`, `sprint`, `subtask`, `story-points` |
| jira-relationships | `jira-as relationships` | `link`, `unlink`, `get-blockers`, `stats` |
| jira-time | `jira-as time` | `log`, `worklogs`, `estimate`, `report` |
| jira-bulk | `jira-as bulk` | `transition`, `assign`, `set-priority`, `delete` |
| jira-dev | `jira-as dev` | `branch-name`, `parse-commits`, `link-pr` |
| jira-fields | `jira-as fields` | `list`, `create`, `configure-agile` |
| jira-jsm | `jira-as jsm` | `request`, `sla`, `approval`, `queue` |
| jira-ops | `jira-as ops` | `cache-status`, `cache-clear`, `discover-project` |

---

*See [CLAUDE.md](/CLAUDE.md) for comprehensive script development guidelines.*
