---
name: lifecycle
description: Where Null's work lives in Linear and what moves when. Reference, loaded on request.
disable-model-invocation: true
allowed-tools: Bash(linear:*)
---

How the skills bind to Linear. Each skill produces an artifact; this reference says where it lives and which state moves. Rigor for each artifact is the skill's; command flags and traps are the `linear` skill's. Every Linear write here happens on the user's word. Approval of spec content is not permission to publish it or change Linear state unless the user's request also authorizes those writes.

Before any Linear write, complete [target binding](#target-binding-states-and-labels).

## The map

| Level | Linear | Artifact | Home |
|---|---|---|---|
| Venture | Initiative and team | Standing purpose and constraints | Initiative description |
| Finite effort | Project | Intent | `agent-docs/intents/<slug>.md` in the venture's repo, linked from the project overview |
| Unit of work | Issue | Spec | Issue description |
| Route | Document on the issue | Plan | Linear Document attached to the issue |
| Record | PR and close-out comment | `pr` skill, close-out below | GitHub, issue comment |
| Lasting design choice | No tracker object required | Design decision | The repository and path named by the project's decision guide |

Before designing, changing, or reviewing an area, use the project's decision guide to find and read its relevant records. For recording or revising a lasting choice, read [decision-record guidance](skill://software-design/DECISIONS.md) for selection, format, evidence, and permissions. If the project has no record home, propose `agent-docs/design-decisions/<slug>.md` in the repository whose design it describes and resolve ownership before writing. That repository need not be the one holding the intent. Project guidance and these records remain usable without invoking this workflow.

## Events

| Event | Skill | Artifact goes | Linear moves |
|---|---|---|---|
| Work arrives | sizing rule below | an issue or a project | `Backlog` if it is not yet sized or specced |
| Project shaped | `shape`, then `intent` | `agent-docs/intents/<slug>.md`, landed on main | project created at `planned`: name is the H1, description is the Goal's first sentence, overview is the link to the file on main, team and `--initiative` are the venture's |
| Intent sliced | `spec` | issue descriptions; omit `Source:` only under `spec`'s source-provenance rule, after confirming the project's overview link resolves to the intent | placeholder to `Backlog`, approved spec to `Todo`, each edge `relation add <id> blocked-by <blocker>`, one label and a priority each |
| Standalone requirement approved | `spec`, standalone path | team-level issue description with a `Source:` link to the approved report or requirement in the first line, no project or intent required | approved spec to `Todo`, one label and a priority |
| Issue picked up | `plan`, unless trivial by its own test | Linear Document on the issue, title `Plan` | issue to `In Progress`; the project's first pickup also moves it to `started` |
| Picked-up scope changes | `spec`, After pickup | approved amendment in the existing issue description, or replacement/follow-on specs in new issues; preserve the records that `spec` requires | amendment keeps the issue `In Progress`; new approved specs to `Todo`; superseded issue to `Canceled`, or `Duplicate` when already covered; revise affected relations only with write permission |
| Building | | branch, as the repo makes branches | |
| A lasting design choice is accepted, at any stage | `software-design`'s decision-record support | project decision record, only with file-write permission; plans and PRs link it | none |
| PR opens | `pr` | the PR | |
| PR merges | | close-out comment | issue to `Done` |
| Project complete | | intent moved to `agent-docs/archive/<slug>.md`, landed on main | overview link repointed (the `projectUpdate` recipe in the `linear` skill), project to `completed` |

## Target binding, states, and labels

Read the project's Linear guide and confirm its workspace, team, project-selection rule, initiative association, and constraints. Inspect the issue states in that team, the labels available to it, and any project statuses needed for the requested event. If the guide says Linear is not used, resolve that with the user before proceeding.

Confirm an event-to-state mapping and permitted label policy for this target. Use the project's adopted workflow mapping when one exists. The names below are defaults; every state reference in this workflow, including Events and Rules, resolves through the confirmed mapping. Bind project statuses separately from team issue states. A category alone does not select a state: when several states share a category, the mapping must name the exact destination for each event.

Binding is complete when every transition has an exact existing destination and issue creation has an available, permitted type label. Resolve missing, ambiguous, or conflicting states and labels with the user before writing. Do not create or rename configuration or silently choose a near match.

No integration moves an issue; every transition is one `linear issue update <ID> --state "<Mapped name>"` at the moment its event fires.

| Event | Default state |
|---|---|
| Captured, or a placeholder published: no approved spec yet | `Backlog` |
| Spec written and approved | `Todo` |
| Picked up, through building and review | `In Progress` |
| PR merges | `Done`, plus the close-out comment |
| Dropped, superseded, or absorbed by a re-slice | `Canceled`, or `Duplicate` when another issue already covers it |

Every issue gets one type label and a priority at creation. Use an existing type label allowed by the confirmed policy. Default labels, only when available and permitted, are `Bug`, `Feature`, `Improvement`, `Chore`, and `Audit`. Priority 1 Urgent drops everything, 2 High is next up, 3 Medium is planned work and the default, 4 Low is nice to have.

The close-out comment is one line, `Done in PR #NN (<merge sha>).`, posted with `issue comment add --body-file`. One extra sentence only when what shipped diverged from the spec; change-specific rationale lives in the PR, which links any lasting design rationale in decision records.

## Rules

- Sizing. One session of work is an issue carrying a spec; more is a project carrying an intent and its stop criteria. A venture is open-ended: no stop criteria, no timeline; only its projects complete.
- An unplanned issue attaches to an active project only when it blocks that project's stop criteria. Otherwise it is team-level with no project. Use `spec`'s standalone path from its approved bug report, GitHub issue, or explicit requirement, and retain its `Source:` reference under that skill's source-provenance rule, including when it attaches to a project. Once the spec is approved, publish it and move the issue to `Todo` only on the user's word.
- Promotion runs both ways. An issue that outgrows a session gets an intent and a project; keep it as the first spec only if its approved contract still fits. Changes to a picked-up contract follow `spec`'s After pickup procedure. A project that collapses to one slice is canceled and the issue kept.
- Each fact has one home. The intent cites the initiative for standing constraints. Blocking order is native relations, never prose in a body. The intent is linked from Linear, never copied into it.
- Publish blockers first, so every edge names a real id.
- Re-slice flat. Every slice is a top-level issue; the hierarchy is the blocking graph. When the frontier reaches a placeholder that is more than one session, re-scope it into the first real slice, create the siblings, and re-examine every edge that pointed at the placeholder: it meant "blocked by all of it," and each dependent now needs a specific sibling.
- Work artifacts freeze at the last responsible moment, on their own clocks: the intent once shaped, the spec at pickup, the plan at pickup, the PR at merge. Before its moment an artifact is malleable; after it, only the cause its skill names reopens it.
- For a proposed change to picked-up requirements, use `spec`'s After pickup procedure for the user's scope decision and the amendment, replacement, or separate follow-on record. Content approval is not permission to edit issue descriptions, create issues, change relations, or move states. Without those permissions, return the proposed records in chat and leave Linear unchanged.
- The plan is frozen at pickup. A changed route is recorded in the PR's Decisions section, never edited into the Document. A dead approach gets a new Document on the same issue, titled `Plan 2`, then `Plan 3`; earlier ones stay as the record of what was tried, and Decisions says why the route changed.
- Design decisions do not freeze at pickup or merge. Revisit them under the shared decision-record guidance when their reasons or constraints change; a better argument requires an explicit revision, not a silent exception.
- One issue per PR.
- The Linear move is always `issue update --state`; `issue start` is not used.
- Completion is the operator's call. When every issue is terminal and the stop criteria appear met, say so and ask. On the word, the three completion actions happen together, in the order the Events row gives.
- Ventures have one repo. When one has several, ask which holds the intent.
- Every project sits in its venture's initiative. When no initiative fits, resolve placement with the user before creating anything.

## Not bound here

`shakedown` runs at any gate on request. `handoff` writes its file and nothing to Linear.
