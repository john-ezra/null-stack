# Git conventions

The hard guardrails live in [AGENTS.md under Rules](../AGENTS.md#rules). This file owns branching, commit, PR, and merge conventions; it grants no permission to publish.

## Branches

Identify the owning repository and its default branch from repository configuration or hosting metadata. If the default branch remains unclear, resolve it with the user before branching or choosing a PR target.

Start feature and fix branches from the default branch. Use `feat/<slug>` for features and `fix/<slug>` for fixes. Include an issue ID only when the work already has one. Continue on an existing branch when it belongs to the requested work; preserve unrelated changes and do not reset the branch to make it match the default.

## Commits

Use Conventional Commits with an imperative subject, 72 characters maximum. Keep each commit focused on one change. Follow any existing signing requirements and hooks; do not bypass them to finish a commit.

Inspect the diff and stage only the intended paths. Review the staged diff before an authorized commit so unrelated work does not enter it.

## Pull requests and merges

Target the default branch unless the user identifies another existing target. Keep each PR focused on one change and, when the work has an issue, one issue. Describe the change, link relevant requirements, and report the checks actually run and any remaining verification gaps.

Follow the repository's existing review requirements and required checks. Resolve failures and outstanding review requests before merging; do not bypass protection rules or claim approval or passing CI without evidence.

When the user authorizes a merge, use squash merge. If repository policy disallows it, resolve the conflict with the user rather than changing repository settings or silently choosing another method.
