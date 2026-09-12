# Linear context
---
This file identifies the project's Linear workspace and team and records project-specific constraints. For Linear commands, read the `linear-cli` skill for CLI mechanics. Artifact formats belong to their owning skills. For artifact placement and state transitions, read the [development policy](DEVELOPMENT.md); its policies apply only if adopted.

Before accessing project records, resolve the workspace and team from the bindings below. An authenticated account or CLI default is not evidence that it is the right destination. If a needed binding is missing or ambiguous, ask the user before accessing that destination. Authorization for writes lives in [AGENTS.md](../AGENTS.md), under Rules.

*This template becomes `agent-docs/LINEAR.md`; its links resolve from there. Fill this guide with confirmed project facts. Italic text is an editing instruction; fenced blocks labeled "Example:" use invented names and are not configuration. Replace the instructions and remove the examples when filled. Do not put credentials or tokens in this file.*

## Project bindings

*State whether this project uses Linear. If it does not, write "Linear is not used for this project" and remove the binding table and constraints section. Do not create a workspace or team to complete this template.*

| Binding | Project value |
| --- | --- |
| Workspace | *Workspace name and URL or slug* |
| Team | *Team name and key; record its stable ID if needed to distinguish it* |
| Project selection | *The existing project name and URL, a rule for selecting among projects, or "No default project; resolve per request"* |
| Initiative association | *The initiative name and URL or "None"; say when it applies if only some work belongs there* |

```
Example:
Workspace: Example Company, slug example-company.
Team: Application, key APP.
Project selection: No default project; resolve per request.
Initiative association: None.
```

## Write permission

*State which tracker writes a request authorizes on its own and which need explicit authorization. Name the exact issue states a pickup and a completion move to, using the team's existing state names; do not rename or create states to fit this template. Keep the rule that questions and inspection requests are read-only.*

```
Example: A request to work on a named issue authorizes moving it to In Progress at pickup and to Done once its acceptance criteria are verified and any required merge has succeeded.

After a PR merges into its intended target branch, update existing Linear artifact links affected by that PR without asking again, including links in previously completed records. Replace links only after the new targets are published and verified. This permission covers link repairs, not new records, new comments, or unrelated content or metadata changes.

Every other write, including project status, relations, and comments, needs authorization in the request. Approval of content is not permission to publish it or change tracker state.
```

## Project constraints

*Record only constraints that differ by project. Fill each item, or say "No project-specific constraint" where none applies. Do not put commands, artifact templates, lifecycle stages, or state-transition rules here.*

- Permitted destinations: *Which teams and projects may hold this repository's work, and any destinations to exclude.*
- Labels and priorities: *Existing required or restricted labels and any project-specific priority policy. Do not invent label names or create labels just to fill this guide.*
- Ownership: *Required assignees or reviewers, or how the user chooses them. Do not infer ownership from the authenticated account.*
- Visibility and sensitive content: *Who can see the destination, what must stay out of Linear, and whether links to repository material are accessible to those readers.*
- Integrations: *Any existing automation that changes records or constrains allowed writes. Record the automation as a project fact, not a lifecycle instruction.*

```
Example:
Permitted destinations: Application team only; do not file this repository's work with the Support team.
Labels and priorities: New issues require one existing type label: Bug, Feature, Improvement, Chore, or Audit. Priority 1 urgent drops everything, 2 high is next up, 3 medium is planned work and the default, and 4 low is nice to have. Preserve existing labels and priorities unless the request authorizes a change. Resolve unavailable labels before creation; do not create them to satisfy this example.
Ownership: Leave new records unassigned unless the user names an owner.
Visibility and sensitive content: The workspace includes external contractors. Do not paste customer data or private incident logs.
Integrations: No automation changes Linear records for this repository.
```
