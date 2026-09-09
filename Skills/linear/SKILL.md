---
name: linear
description: "Linear CLI mechanics. Use for any `linear` command, publishing or replacing Linear bodies, reconciling issue relations, or applying authorized tracker transitions; includes the GraphQL fallback when no flag covers an operation."
disable-model-invocation: false
allowed-tools: Bash(linear:*), Bash(curl:*)
---

How to drive the `linear` CLI. Artifact semantics belong to their owning skills; project policy or the user's request chooses destinations and state transitions. This skill executes authorized writes, not lifecycle decisions. For changed spec dependencies, get the approved blocking order from `spec`; for post-merge evidence and close-out content, use `pr`.

## The repo pin

A repo is Linear-tracked when its root holds `.linear.toml`, which supplies the default workspace and team for commands that use them:

```toml
workspace = "<workspace-slug>"
team_id = "<TEAM-KEY>"
```

`linear config` generates it interactively. `linear auth whoami` checks the login; if it fails, the user runs `linear auth login` themselves.

## Markdown goes through files

Any flag that takes markdown has a file form. Use it for anything longer than one line; inline flags mangle newlines and shell-escape badly.

| Command | File flag |
|---|---|
| `issue create`, `issue update` | `--description-file` |
| `issue comment add`, `issue comment update` | `--body-file` |
| `project create` | `--content-file` (overview) |
| `document create`, `document update` | `--content-file` |

## Recipes

Query issues. `issue list` is an alias of `issue mine` and shows only your issues; `issue query` covers a team or project:

```bash
linear issue query --project "<project>" --state unstarted --json
linear issue query --team WEB --label Bug --updated-after 2026-01-01
```

Create an issue, one label and a priority, into a project:

```bash
linear issue create --title "<imperative title>" --description-file ./spec.md \
  --project "<project>" --label Feature --priority 3 --state Todo --no-interactive
```

Move state, comment, wire a blocking edge:

```bash
linear issue update WEB-12 --state "In Progress"
linear issue comment add WEB-12 --body-file ./comment.md
linear issue relation add WEB-14 blocked-by WEB-12
linear issue relation list WEB-14
```

Create a project under an initiative with an overview:

```bash
linear project create --name "<name>" --team WEB --initiative "<initiative>" \
  --description "<one sentence, 255 chars max>" --content-file ./overview.md --status planned
linear project update <project> --status started
```

Attach a document to an issue or project:

```bash
linear document create --issue WEB-12 --title Plan --content-file ./plan.md
linear document update <document> --content-file ./plan.md
```

Inline image in a comment:

```bash
linear issue comment add WEB-12 --attach ./screenshot.png
```

## Writes

Read the project's Linear guide when one exists for identities, labels, priorities, visibility, and integration constraints. Confirm the requested writes separately from content approval. With no write permission, return the proposed changes without touching Linear. A repo pin selects defaults, not authority.

When a requested transition names an issue state, resolve the exact existing state in the bound team; resolve project statuses separately. A state category does not select among several names in that category. Confirm required labels exist and are allowed by project policy. Resolve missing or conflicting choices with the user rather than creating or renaming configuration, choosing a near match, or overwriting unrelated labels and priorities.

- **Confirm the target first.** With no `.linear.toml` at the repo root, pass `--workspace <slug>` explicitly on writes instead of trusting whatever workspace `linear auth default` last set. Add `--team <key>` only when the command's help documents it and its meaning matches the intended operation. `issue comment add` has no `--team`; `document update --team` changes the document's attachment, not its workspace scope. Then confirm the identifier in the intended workspace is the thing you mean: `linear issue view WEB-12 --json` and read the title before `issue update`, `comment add`, or `relation add` touches it.
- **Replace a body from its current version.** Issue descriptions, Documents, comments, and project overviews have whole-body replacement paths. Fetch the current body and attachments needed to identify it before editing: `issue view <id> --json`, `document view <id> --json`, or `project(id:) { content }` through `linear api` for an overview. For a comment, discover its read operation through command help or the schema. Edit that copy, preserving unrelated content and the owning skill's frozen history. Fetch again before replacing; if the body changed, reconcile rather than overwrite. After writing, fetch the result and compare it with what you sent. Use the file flags above or the documented GraphQL fallback. `document update` stops when inline comments would lose their anchors; use `--force` only after the user authorizes it.
- **Confirm results, including partial writes.** Check the created record, attachment, relation, or state at its destination. For a multi-write operation, keep the confirmed identifiers and report which actions succeeded, which failed, and which remain. Stop dependent writes when their prerequisite fails. Before resuming, inspect the current records so a successful comment or Document is not created twice.

## Reconcile issue relations

Use this path when authorized changes split, merge, replace, cancel, or otherwise change related issues. The approved work breakdown supplies the desired dependencies and terminal dispositions; this procedure only applies them.

1. Read the affected issues and list their relations, including issues that block them and dependents they block. Confirm both endpoints in the intended workspace and team context. Compare the current edges with the approved graph. Done when every affected edge is identified and unrelated edges are excluded from the edit set.
2. Publish approved blockers before their dependents where possible, then create relations only after both endpoints have confirmed identifiers. Reuse records already published on a partial attempt. Use `issue relation add <dependent> blocked-by <blocker>` for that direction; inspect help for removal syntax, or the schema when the CLI lacks the operation. Do not guess identifiers or swap the endpoints.
3. For dependents that will remain active, add and confirm required replacement edges before removing obsolete ones, so a failed write cannot leave them falsely unblocked. If this ordering would temporarily create a cycle, stop for a safe staged graph decision instead of applying it. Preserve unrelated relations.
4. Before applying a requested terminal disposition, reconcile dependents that will remain active, confirm terminal dispositions for dependents being discarded, and record any required replacement reference. Confirm the issue's terminal state before removing its own obsolete blocker edges; if that state write fails, leave those edges intact. A terminal state does not satisfy a missing deliverable.
5. Read back the changed relations from both endpoints and any requested terminal states. Done when the actual graph matches the approved graph, no dependent retains a misleading edge to a discarded slice, and no unrelated relation changed. Report any partial result rather than claiming reconciliation finished.

## Traps

- `issue comment create` does not exist; the verb is `add`.
- `issue start` creates and checks out a git branch as a side effect. Move state with `issue update --state`.
- `issue attach` makes a sidebar link and never renders an image inline; `comment add --attach` does.
- `project update` has no `--content` or `--content-file`. Changing an overview after creation is the GraphQL fallback below.
- `project view` has no `--json`; a project's overview is read through the GraphQL fallback.
- `project --description` is capped at 255 characters by the API; the overview (`--content-file`) is not.
- `issue query --state` and `issue list --state` filter by state type, never by name: `backlog`, `unstarted`, `started`, `completed`, `canceled`, `duplicate`. When a team has two states of one type, read `state.name` in the JSON to tell them apart.
- `--no-pager` exists only on `issue list` and `issue query`; other commands error on it.
- `issue list` needs `--team <key>` unless the repo pin supplies it.

## Reference

`linear <command> --help` lists a command's subcommands and `linear <command> <subcommand> --help` its flags; both are the installed version's own text, so nothing here repeats them. The commands are `api`, `auth`, `config`, `cycle`, `document`, `initiative`, `initiative-update`, `issue`, `label`, `milestone`, `project`, `project-update`, `schema`, `team`, and `user`. Curated examples for initiatives, labels, projects, and bulk operations are in [references/organization-features.md](references/organization-features.md).

## GraphQL fallback

Reach for `linear api` only when no command or flag covers the operation. Find the shape in the schema first:

```bash
linear schema -o "${TMPDIR:-/tmp}/linear-schema.graphql"
grep -A 30 "^input ProjectUpdateInput" "${TMPDIR:-/tmp}/linear-schema.graphql"
```

A query with non-null markers (`String!`) goes through a heredoc; inline quoting breaks on the `!`:

```bash
linear api '{ viewer { id name } }'

linear api --variable id=<project-id> --variable content="$(cat ./overview.md)" <<'GRAPHQL'
mutation($id: String!, $content: String!) {
  projectUpdate(id: $id, input: { content: $content }) { success }
}
GRAPHQL

linear api --variables-json '{"filter": {"state": {"name": {"eq": "In Progress"}}}}' <<'GRAPHQL'
query($filter: IssueFilter!) { issues(filter: $filter) { nodes { identifier title } } }
GRAPHQL
```

Raw HTTP, when the CLI's `api` command is not enough. Pass the authorization header through stdin with `-H @-` so the token stays out of process arguments. Keep shell tracing and curl verbose/trace output off when handling credentials.

```bash
curl -s -X POST https://api.linear.app/graphql \
  -H "Content-Type: application/json" \
  -H @- \
  -d '{"query": "{ viewer { id } }"}' <<EOF
Authorization: $(linear auth token)
EOF
```
