# Git conventions
---
The hard guardrails live in [AGENTS.md](../AGENTS.md), under Rules. This file owns the project's branching, commit, PR, and merge conventions.

*This template becomes `agent-docs/GIT.md`; its links resolve from there. Fill each section with this project's conventions. Keep examples only as a guide while editing, then delete them. Remove sections that do not apply.*

## Branches

*Name the base branch, branch naming pattern, and any release or maintenance branches. Say whether branch names include tracker IDs; do not require a tracker merely to fill this template.*

```
Example: Branch from main. Use <kind>/<short-kebab-case-description> with feat, fix, docs, refactor, or chore. Keep tracker IDs out of branch names.
```

## Commits

*Give the commit message format and any project-specific grouping or signing requirements.*

```
Example: Write a plain imperative subject without a type prefix, 72 characters maximum, that completes "If applied, this commit will...". Keep each commit focused on one change.
```

## Pull requests and merges

*Give the target branch, scope, required review and checks, merge method, and any release requirements. These conventions describe how authorized publication works; they do not authorize it.*

```
Example: Target main. Use one issue per PR when work has an issue; otherwise keep the PR focused on one change. Require one approval and passing CI, then squash-merge.
```

## Branch cleanup

*Say whether merged task branches are deleted after closeout without a separate request, and what must be confirmed first. If the project keeps branches, say so and remove the checks.*

```
Example: After an authorized closeout, delete the task's merged branches locally and remotely. Confirm the PR merge, a clean working tree, no unpushed work, and that the branch tip matches the merged PR head before deleting. Never delete the default branch or unrelated branches.
```
