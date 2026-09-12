# Git conventions
---
The hard guardrails live in [AGENTS.md](../AGENTS.md), under Rules. This file owns the project's repository layout, branching, worktree, commit, PR, and merge conventions, including publication permission.

*This template becomes `agent-docs/GIT.md`; its links resolve from there. Fill each section with this project's conventions. Keep examples only as a guide while editing, then delete them. Remove sections that do not apply.*

## Publication

*State when completed work must be committed and pushed, when to open or update a PR, and which operations still need explicit approval. Distinguish a verified change from a finished issue, cover work without an issue, and say how a request to defer publication overrides the default.*

```
Example: Commit and push each completed, verified change on its task branch without asking again, even while the issue has work remaining. Open or update a ready-for-review PR once the issue's implementation, verification, and documentation are complete; do not wait for Done. Without an issue, use completion of the full requested scope. Merging, amending, rebasing, and force-pushing require explicit approval. Honor requests to keep work local or defer publication. If verification or publication is blocked, preserve the work and report the blocker.
```

## Repositories

*Name each repository the work touches and what it owns. If the code lives in a separate repository, such as a submodule of this workspace, say where Git commands run for each, how to branch inside the submodule, and the order in which a change spanning both is published. Remove this section for a single repository.*

```
Example: This workspace is the private repository; the code is a submodule at `app/` with its own history and PRs. Agent guidance, agent docs, workflows, and worktrees stay here. Identify the owning repository from the changed paths before any Git write, and branch inside the submodule before editing it. Land the code PR first, record its merged commit in the workspace gitlink, then land the workspace PR.
```

## Branches

*Name the default branch for each repository explicitly, such as `main` or `master`, along with the branch naming pattern and any release or maintenance branches. For new repositories, say to create the default branch before creating a task branch. Say whether branch names include tracker IDs; do not require a tracker merely to fill this template.*

```
Example: Use main as the default branch for new repositories and create it before creating any task branch. For existing repositories, use the default branch recorded in repository configuration or hosting metadata, such as master; if unclear, ask the user. Do not infer the default from the current or first-created branch. Branch from the default. Use <kind>/<short-kebab-case-description> with feat, fix, docs, refactor, or chore. Keep tracker IDs out of branch names.
```

## Worktrees

*Say when a linked worktree is justified rather than switching branches, where worktrees live and how their directories are named, and when and how they are removed. Name the ignored directory so the location travels with the repository.*

```
Example: Use a worktree only when a second checkout is needed at the same time. Create them under `.worktrees/` at the repository root, which `.gitignore` excludes, named for the branch with `/` replaced by `-`. Remove a worktree with `git worktree remove` when its work is closed out or abandoned, before deleting its branch. Leave worktrees you did not create alone.
```

## Commits

*Give the commit message format and any project-specific grouping or signing requirements.*

```
Example: Write a plain imperative subject without a type prefix, 72 characters maximum, that completes "If applied, this commit will...". Keep each commit focused on one change.
```

## Pull requests and merges

*Give the target branch, scope, required review and checks, merge method, whether the merge deletes the branch, and any release requirements. Keep publication triggers and permissions in Publication above.*

```
Example: Target the repository's default branch. Use one issue per PR when work has an issue; otherwise keep the PR focused on one change. Require one approval and passing CI, then squash-merge and delete the branch locally and remotely in the same action.
```

## Branch cleanup

*Say what cleanup remains after the merge, such as the task's worktrees and any branch a merge left behind, whether it happens without a separate request, and what must be confirmed first. If the project keeps branches, say so and remove the checks.*

```
Example: After an authorized closeout, remove the task's worktrees and delete any of its merged branches the merge left behind, locally and remotely. Confirm the PR merge, a clean working tree, no unpushed work, and that the branch tip matches the merged PR head before deleting; a squash-merged branch needs `git branch -D`. Never delete the default branch or unrelated branches.
```
