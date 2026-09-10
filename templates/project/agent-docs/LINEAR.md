# Linear context
---
This file identifies the project's Linear workspace and team and records project-specific constraints. For Linear commands, read the `linear` skill for CLI mechanics. Artifact formats belong to their owning skills. For artifact placement and state transitions, read the [development lifecycle](DEVELOPMENT.md); its policies apply only if adopted.

Before accessing project records, resolve the workspace and team from the bindings below. An authenticated account or CLI default is not evidence that it is the right destination. If a needed binding is missing or ambiguous, ask the user before accessing that destination. Authorization for writes lives in [AGENTS.md](../AGENTS.md), under Rules.

*Fill this guide with confirmed project facts. Italic text is an editing instruction; fenced blocks labeled "Example:" use invented names and are not configuration. Replace the instructions and remove the examples when filled. Do not put credentials or tokens in this file.*

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
