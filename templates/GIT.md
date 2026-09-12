# Git conventions
---
The hard guardrails live in [AGENTS.md](../AGENTS.md), under Rules. This file owns the project's branching, commit, PR, and merge conventions.

*This template becomes `agent-docs/GIT.md`; its links resolve from there. Fill each section with this project's conventions. Keep examples only as a guide while editing, then delete them. Remove sections that do not apply.*

## Branches

*Name the base branch, branch naming pattern, and any release or maintenance branches. Say whether branch names include tracker IDs; do not require a tracker merely to fill this template.*

```
Example: Branch from main. Use feat/<slug> for features and fix/<slug> for fixes. Add an issue ID only when the work already has one.
```

## Commits

*Give the commit message format and any project-specific grouping or signing requirements.*

```
Example: Use conventional commits with an imperative subject, 72 characters maximum. Keep each commit focused on one change.
```

## Pull requests and merges

*Give the target branch, scope, required review and checks, merge method, and any release requirements. These conventions describe how authorized publication works; they do not authorize it.*

```
Example: Target main. Use one issue per PR when work has an issue; otherwise keep the PR focused on one change. Require one approval and passing CI, then squash-merge.
```
