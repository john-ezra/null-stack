# Git conventions

The hard guardrails live in [AGENTS.md under Rules](../AGENTS.md#rules). This file owns repository layout, branching, worktree, commit, PR, and merge conventions, including publication permission.

## Publication

Commit and push each completed, verified change on its task branch without asking again, even when the issue still has work remaining. Include only the authorized change, not unfinished or unrelated work.

Open a ready-for-review PR once the issue's implementation, verification, and required documentation are complete, or update the existing PR for that work. Do not wait for the issue to reach Done or for another publication request. For work without an issue, use completion of the full requested scope as the trigger. Follow the [two-repository publication order](#repositories) for work spanning both repositories.

Merging, amending commits, rebasing, and force-pushing still require explicit approval. A request to keep work local or defer publication overrides these defaults. If verification or publication is blocked, preserve the work and report the blocker rather than claiming completion.

## Repositories

This workspace is the private repository. The project's code is a Git submodule with its own repository, history, and pull requests, checked out at the path `.gitmodules` records. Agent guidance, agent docs, workflows, tracker configuration, and worktrees stay in the workspace; keep them out of the project repository.

Before any Git write, identify the owning repository from the paths that change and run Git commands in that repository's checkout. A submodule checkout can sit on a detached HEAD because the workspace records a commit, not a branch; create or select the task's branch inside the submodule before editing project files. Project commits and PRs must make sense without access to the workspace, so do not link workspace files or artifacts from them.

For a change that spans both repositories, land the project PR first and confirm the commit that landed it; the feature branch head is not the delivered revision. Record that commit in the workspace's gitlink, then land the workspace PR with the pointer update and related private changes. Never point the workspace at an unpublished project commit. Workspace-only changes need no project commit or PR.

After a workspace update, `git submodule update --init --recursive` from the workspace root brings a clean project checkout to the recorded revision. Do not discard local work to make it succeed.

## Branches

Use a short-lived branch for every change, including routine maintenance and documentation-only work. Create or select the task's branch before the first repository edit; never edit on the default branch.

Use `main` as the default branch when initializing either repository, and create it before creating any task branch.

For an existing repository, identify the default branch from repository configuration or hosting metadata, preserving names such as `master`. Do not infer the default from the current or first-created branch. If it remains unclear, resolve it with the user before branching or choosing a PR target. Start new task branches from their intended target, normally the default branch.

Name branches `<kind>/<short-kebab-case-description>`, using `feat`, `fix`, `docs`, `refactor`, or `chore`. Keep tracker associations in the tracker rather than in branch names.

Continue on an existing branch when it belongs to the requested work. Preserve unrelated changes rather than resetting or discarding them to prepare a branch. When a branch needs the target's newer commits, merge the target into it rather than rebasing; history rewriting requires explicit permission.

## Worktrees

Switch branches in the current checkout unless the work needs a second checkout at the same time, such as agents working on different branches in parallel or a side-by-side comparison of two branches. Before adding a worktree, check `git worktree list` and reuse the one already holding that branch.

Create every worktree under `.worktrees/` at the workspace root, which the workspace's `.gitignore` excludes. Name the directory for the branch with `/` replaced by `-`. Nest the project repository's worktrees under its submodule path so the two repositories cannot collide:

```sh
git worktree add .worktrees/feat-login feat/login
git -C <project> worktree add ../.worktrees/<project>/feat-login feat/login
```

Remove a worktree with `git worktree remove` when its branch's work is closed out or abandoned, and before deleting the branch; Git refuses to delete a branch that a worktree has checked out. Run `git worktree prune` for registrations whose directories are gone. Leave the main checkouts and worktrees you did not create alone; removing them requires explicit permission. Worktrees the agent harness manages for isolated tasks follow its own location and cleanup.

## Commits

Write a plain imperative subject without a type prefix, at most 72 characters. It must complete the sentence "If applied, this commit will...".

Inspect the diff and stage only the intended paths, then review the staged diff before an authorized commit so unrelated work does not enter it. Follow the repository's signing requirements and hooks; do not bypass them to finish a commit.

## Pull requests and merges

Land changes through pull requests. Target the default branch unless the user identifies another existing target. Keep each PR to one coherent, independently reviewable change, normally one issue or spec. Include related documentation and artifact updates with the change they support; keep unrelated maintenance out even when it happened in the same session.

Use `pr` for titles, bodies, and delivery evidence. A PR must make sense without tracker access; keep the association on the tracker side, as [Linear context](LINEAR.md#constraints) describes.

Honor the repository's required reviews and checks. Verify their results before merging; do not bypass protection rules or claim approval or passing checks without evidence.

When the user authorizes a merge, squash merge and delete the task branch remotely and locally as part of the merge. On GitHub, run `gh pr merge --squash --delete-branch`, then switch the checkout to the default branch, fast-forward it, and delete the local task branch with `git branch -D` if it still exists; `gh` skips the local delete when it cannot switch the checkout, as in a submodule checkout, and says so. No separate check is needed, because at that moment the branch tip is the merged head. Use another merge method only on explicit request. If repository policy disallows squash merging, resolve that with the user rather than changing settings or silently choosing another method.

## Branch cleanup

The merge deletes the task branch. This section covers what it cannot: the task's worktrees, and a merged branch found afterwards, from a merge made without deleting it or an earlier session. Successful authorized closeout includes removing those locally and remotely, without a separate deletion request. This standing permission covers only that task's worktrees and branches, never the main checkouts, the default branch, or unrelated ones.

Before deleting a branch after the fact, confirm the actual PR merge, a clean working tree, no unpushed work, and no commits added to the branch after the revision that was merged. For squash merges, compare the branch tip with the confirmed PR head rather than relying on commit ancestry; `git branch -d` refuses a squash-merged branch, so use `-D` once the tip matches. If any check fails, preserve the worktree and branch and report the pending cleanup.
