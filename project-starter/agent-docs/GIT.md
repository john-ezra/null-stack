# Git conventions

The hard guardrails live in [AGENTS.md under Rules](../AGENTS.md#rules). This file owns branching, commit, PR, and merge conventions; it grants no permission to publish.

## Branches

Use a short-lived branch for every change, including routine maintenance and documentation-only work. Create or select the task's branch before the first repository edit; never edit on the default branch.

Identify the owning repository and its default branch from repository configuration or hosting metadata. If the default branch remains unclear, resolve it with the user before branching or choosing a PR target. Start new task branches from their intended target, normally the default branch.

Name branches `<kind>/<short-kebab-case-description>`, using `feat`, `fix`, `docs`, `refactor`, or `chore`. Keep tracker associations in the tracker rather than in branch names.

Continue on an existing branch when it belongs to the requested work. Preserve unrelated changes rather than resetting or discarding them to prepare a branch. When a branch needs the target's newer commits, merge the target into it rather than rebasing; history rewriting requires explicit permission.

## Commits

Write a plain imperative subject without a type prefix, at most 72 characters. It must complete the sentence "If applied, this commit will...".

Inspect the diff and stage only the intended paths, then review the staged diff before an authorized commit so unrelated work does not enter it. Follow the repository's signing requirements and hooks; do not bypass them to finish a commit.

## Pull requests and merges

Land changes through pull requests. Target the default branch unless the user identifies another existing target. Keep each PR to one coherent, independently reviewable change, normally one issue or spec. Include related documentation and artifact updates with the change they support; keep unrelated maintenance out even when it happened in the same session.

Use `pr` for titles, bodies, and delivery evidence. A PR must make sense without tracker access; keep the association on the tracker side, as [Linear context](LINEAR.md#constraints) describes.

Honor the repository's required reviews and checks. Verify their results before merging; do not bypass protection rules or claim approval or passing checks without evidence.

When the user authorizes a merge, use squash merge. Use another method only on explicit request. If repository policy disallows squash merging, resolve that with the user rather than changing settings or silently choosing another method.

## Branch cleanup

Successful authorized closeout includes deleting the task's merged branches locally and remotely, without a separate deletion request. This standing permission covers only that task's branches, never the default branch or unrelated branches.

Before deletion, confirm the actual PR merge, a clean working tree, no unpushed work, and no commits added to the branch after the revision that was merged. For squash merges, compare the branch tip with the confirmed PR head rather than relying on commit ancestry. If any check fails, preserve the branch and report the pending cleanup.
