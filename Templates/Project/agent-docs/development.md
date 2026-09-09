# Development lifecycle authoring template

This file is authoring material, not adopted policy or a runnable workflow. Reading or copying it authorizes no execution or publication. Until the project makes an explicit choice, report that no lifecycle is selected.

## Author the project guide

1. Choose an adopted lifecycle, an explicit absence of one, or a relative link to another project-owned policy. Use one of the bounded blocks below as a starting point. The finished `agent-docs/development.md` holds project decisions and conditional pointers, not this authoring document with a few notes removed.
2. Confirm entry thresholds, authoritative artifact homes, approval and write-policy choices, tracker event mapping, resizing, and effort completion. The finite-effort example is one choice, not a requirement. If the project does not use Linear, replace its tracker choices rather than inventing bindings. Read [Linear context](linear.md) for identities, labels, priorities, visibility, and integrations; put those facts there, not in this policy.
3. Read the owning skills before adopting the example's integrations. Keep slicing and requirement history in `spec`, plan decisions and replacements in `plan`, intent revisions in `intent`, PR evidence and close-out in `pr`, tracker mechanics in `linear`, and session-transfer construction in manual `handoff`. Preserve their approval boundaries. No workflow or tracker is required for standalone skill use.
4. Keep Git choices in [git.md](git.md), including PR scope and the landing branch, and lasting-decision rules in [design-decisions/README.md](design-decisions/README.md). Resolve conflicts with [project write restrictions](../AGENTS.md#6-rules) rather than repeating or weakening them. Confirm every artifact's owning repository when an effort spans repositories.
5. Replace this entire file with the chosen block's adapted content, without its outer fence. Finish when all project choices are explicit, authoring instructions and unused examples are gone, retained links and anchors work from the consuming project, and no host-specific resource URI or toolkit-checkout path is required. The ordinary finished guide should be roughly 400-700 words; policy complexity, not a word quota, decides its length. Merely copying either example does not adopt it.

## Option: no lifecycle selected

Retain only the following block if the project chooses this option.

```markdown
# Development lifecycle

No development lifecycle is selected for this project. Use only the requested skill or project guide; do not infer tracker records, artifact homes, or task transitions. Resolve any destination or permission needed for that request before writing. Reading this guide does not authorize execution or publication.

Before Git or PR work, read [Git conventions](git.md). Before Linear access, read [Linear context](linear.md). Before design, change, review, or decision-record maintenance, read [design decisions](design-decisions/README.md). [Project write restrictions](../AGENTS.md#6-rules) still apply.
```

## Filled example: finite efforts with Linear

These are example project choices, including state names. Confirm them before adoption. Retain only the adapted block.

```markdown
# Development lifecycle

We use the finite-effort policy below. It selects no task workflow and grants no permission to execute or publish. Apply only the requested event; finishing one does not authorize the next.

## Authority and owners

Content approval and write permission are separate. Follow [project write restrictions](../AGENTS.md#6-rules); file creation or editing, PR creation, merge, and archival also need explicit authorization. Use authorization already present in the request. Without it, return the draft and proposed destination in chat. Report completed and outstanding writes after a failure.

Before Git or PR work, read [Git conventions](git.md). Before Linear access, read [Linear context](linear.md) for identities, labels, priorities, visibility, and integrations. Before design, change, review, or record maintenance, read [design decisions](design-decisions/README.md).

Use `intent` for intents and revisions; `spec` for slicing, provenance, dependency decisions, and frozen-scope changes; `plan` for skip decisions and replacement plans; `pr` for PRs and post-merge close-out; `linear` for tracker writes and relation reconciliation. Suggest manual `handoff` for session transfer. Critique may use `shakedown`; neither critique nor transfer changes tracker state.

## Entry and homes

One session takes one spec issue. Larger finite work needs an intent and Linear project; standing work has no completion criteria or timeline. Approved standalone requirements may enter through `spec` without either. Attach unplanned work to an active project only if it blocks the intent's stop criteria; otherwise keep it team-level. A skill-only request creates no tracker obligation.

Repository paths start at the owning repository root. Confirm that repository for each artifact, including cross-repository work. Git conventions choose the landing branch.

| Artifact | Authoritative home |
|---|---|
| Standing purpose, when an initiative is selected | Existing initiative description; intents cite it |
| Intent | `agent-docs/intents/<slug>.md`, landed on the default branch |
| Spec | Linear issue description; apply `spec`'s provenance rule |
| Blocking order | Native issue relations; use sibling issues, not subtask trees |
| Plan | Issue-attached Linear Document, named under `plan` |
| Implementation and proof | Owning repository change and PR |
| Completed intent | `agent-docs/archive/<slug>.md`, landed on the default branch |

Project overviews link the authoritative intent, never a second copy. Create a finite-effort project only after its approved intent lands; use its title and the Goal's first sentence for the project name and short description. Apply the initiative choice from Linear context. Drafts are working copies, not authoritative records.

## Gates and tracker mapping

Use exact existing destinations confirmed through `linear`. Issue states and project statuses are separate. Transitions are explicit, not triggered by branches or PR integrations.

| Authorized event | Issue state | Project status |
|---|---|---|
| Unapproved capture or coarse placeholder | `Backlog` | No change |
| Approved intent landed and project created | None | `planned` |
| Approved frontier or standalone spec published | `Todo` | No change |
| Pickup with blockers satisfied and plan or skip decision | `In Progress` | `started` on first pickup |
| Implementation, review, PR opening, or approved amendment | Remain `In Progress` | No change |
| Approved replacement or follow-on spec published | `Todo` for new issue | No change |
| Actual merge and `pr` close-out, with acceptance criteria satisfied | `Done` | No change |
| User drops or supersedes work | `Canceled`, or `Duplicate` when covered elsewhere | No change |

Planning alone is not pickup. Implementation owes every approved acceptance criterion; report unmet criteria rather than completion.

## Resizing and completion

An issue exceeding one session becomes a finite effort. Retain it as the first spec only if its approved contract fits. For an effort reduced to one slice, user authorization permits detaching the surviving issue and canceling the redundant project at `canceled`; preserve the intent and history unless separately authorized to move it. Use `spec` and `linear` for affected dependencies and scope records.

When all issues are terminal and the intent's stop criteria are met, present evidence for the operator's completion decision. With approval and permission for every write, land the intent's archive move, then repoint the overview to that landed file, then set the project to `completed`. Terminal issues alone never complete an effort.
```
