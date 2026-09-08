---
name: project-workflow
description: An annotated, optional example for organizing a project's development work in Linear.
disable-model-invocation: true
---

## Adapt before use

This is a template for a project-owned workflow, based on the shared `lifecycle` workflow. Copying the project starter does not adopt this process. Use this file only when the user explicitly requests it; reading it to review or adapt the example does not start work. The individual skills and project guides remain usable without this workflow. Adapting this file changes the consuming project's process, not the shared skills or workflow.

1. Choose which example policies below the project wants to keep. Replace the artifact homes, sizing rule, state mapping, and completion procedure here when adopting different policies. Keep artifact content and format in the owning skills and support files. Adaptation is done when the retained rules describe the project's actual process rather than choices left to the agent.
2. Before binding this workflow to Linear, read [agent-docs/linear.md](../agent-docs/linear.md). Resolve its workspace, team, project-selection rule, initiative association or explicit absence, and project-specific constraints. If the guide says Linear is not used, adapt this example before running it. Binding is done when the target is unambiguous and the states and labels this workflow uses exist in that target; missing configuration is a decision for the user, not permission to create it.
3. Before choosing a branch, landing an artifact, opening a PR, or merging, read [agent-docs/git.md](../agent-docs/git.md). Use its branch, base, review, and publication conventions. Git setup is done when the intended repository and landing branch are known. This example calls that branch the default branch; it does not assume its name is `main`.
4. Keep `workflows/` as the template container when invoking this file by path. Registration is optional. To register it as a packaged skill, choose a unique lowercase name, set `name` to it, and rename the directory to match. Update the project `AGENTS.md` link and any other references to the new path. Keep `disable-model-invocation: true`; use the host's supported skill-discovery location. Packaging is done when the name and directory match and the user's chosen invocation reaches this file. Hiding a skill is not access control or write authorization.

Example invocation without registration: "Use `workflows/SKILL.md` for this issue. Draft the spec here in chat; do not publish it or change tracker state."

Example invocation after registration: the user invokes `/skill:<chosen-name>` on a host that supports skill commands. Registration is not required for explicit invocation by file path.

The relative guide links above resolve from this file. Every runtime path below, including `agent-docs/intents/<slug>.md`, resolves from the consuming repository root, never from `workflows/` or this toolkit's checkout.

## Example policy: authority and skill composition

Follow only the part of this workflow the user requested. Finishing an artifact does not authorize the next event. Use authorization already present in the request; ask only for a missing decision or permission that blocks the requested work.

Content approval, including acceptance of a design decision, and permission to write are separate. Agreement with a draft does not authorize creating or editing a file, publishing a Linear issue or Document, changing a relation or state, pushing a branch, opening a PR, merging, or archiving an intent. A request may authorize several named writes together. Stay within that scope, confirm the destination, and report what actually changed. Without write permission, present the draft and proposed destination in chat and leave the destination untouched. If a write fails, report the completed actions and the remaining action rather than claiming the event finished.

When an event needs an artifact, read the owning skill or support file named below and follow its content rules. This file decides placement and process; it contains no substitute artifact templates.

Before designing, changing, or reviewing an area, or creating or revising a design-decision record, read the [project decision guide](../agent-docs/design-decisions/README.md) for the local home and discovery, and [decision-record guidance](skill://software-design/DECISIONS.md) for the shared rules. Reading that support file does not invoke the full `software-design` skill.

| Condition | Skill and responsibility | Destination and completion |
|---|---|---|
| The idea still needs decisions | `shape` conducts the interview | Decisions and parked questions stay in chat, or in the user-authorized capture document; finish by the skill's decision-frontier test. |
| The user wants a finite effort captured | `intent` writes the want and stop criteria | Draft in chat until file writes are authorized; the approved intent's home is in the artifact map below. |
| An intent or approved standalone requirement needs session-sized work | `spec` defines deliverables and acceptance criteria | Present the breakdown and completed specs for approval; publish only through the corresponding event below. |
| An approved spec is being picked up | `plan` decides whether a route needs writing | Record the skip reason in chat for trivial work, or prepare a plan that passes the skill's cold-successor test. |
| A lasting design choice emerges during shaping, planning, or implementation, or an existing record needs revision | [Decision-record guidance](skill://software-design/DECISIONS.md) owns selection, format, and maintenance | Draft or update the record at the project guide's home within the user's authorization. Recording adds no gate or tracker transition. |
| A PR is requested | `pr` owns its title, body, change-specific rationale, and verification evidence | Draft for review or publish to the repository's PR host as authorized; link lasting rationale in design-decision records and finish by the skill's completion test. |
| Any Linear command is needed | `linear` owns CLI mechanics and safe target handling | Read the skill before the command; use the project guide for bindings and this workflow for the requested event. Confirm the resulting artifact, relation, or state. |

When the user requests `shakedown` at any gate, use that skill on the named target. Its results stay in chat unless the user authorizes capture in that target. Finish with what held, changed, and remains open; it causes no tracker transition and is not a required gate.

When the user wants a cold successor session, suggest `handoff` for the user to invoke. Do not invoke it automatically at a stage boundary. On explicit invocation, its file goes to the handoff directory named by project context; when none is named, ask for the destination as the skill requires. Completion is the delivered absolute file path after its resume and redaction checks. A handoff writes nothing to Linear and does not move the issue out of its current state.

## Example policy: artifact homes

The work-artifact homes below are choices for this workflow, not requirements of the skills or project starter. The project decision guide owns lasting design records independently of this workflow.

| Artifact | Authoritative home | Other references |
|---|---|---|
| Standing purpose and constraints, when the project uses an initiative | Existing Linear initiative description selected by the project guide | The intent cites it rather than copying it. No initiative is required when the guide explicitly selects none. |
| Intent for a finite effort | `agent-docs/intents/<slug>.md`, landed on the default branch | Work-scoping decisions stay in the intent. The Linear project overview links to the file on that branch; it does not carry a second copy. |
| Spec for one unit of work | Linear issue description | The project association identifies an intent-backed source; a standalone spec keeps its source reference in the body. |
| Blocking order | Native Linear issue relations | Publish blockers first, then create relations using their confirmed identifiers; do not repeat the graph in spec bodies. |
| Implementation plan | Linear Document attached to the issue, initially titled `Plan` | A later abandoned approach gets `Plan 2`, then `Plan 3`, on the same issue. |
| Lasting design choice | The repository and path named by the [project decision guide](../agent-docs/design-decisions/README.md) | Plans and PRs link the record rather than copying its rationale. |
| Implementation and verification evidence | Repository change and PR | The PR records change-specific rationale and observed proof using `pr`, linking lasting rationale in design-decision records; the issue receives a close-out comment after merge. |
| Completed intent | `agent-docs/archive/<slug>.md`, landed on the default branch | The project overview points to the archived file. |

Drafts in chat or temporary publication files are working copies, not additional authoritative homes. Read the current authoritative version before replacing a published body; use `linear` for the replacement procedure.

## Example policy: entry and sizing

Choose the entry that matches the request instead of running every skill in sequence.

- An unclear idea goes to `shape` only when shaping is requested or needed to settle the idea. An already clear want can go straight to `intent`.
- One session of work is an issue carrying a spec. More than one session is a finite effort carrying an intent and a Linear project. Open-ended standing work belongs to the project's existing purpose and constraints; only finite efforts have completion criteria.
- An approved bug report, GitHub issue, or explicit requirement can enter through `spec`'s standalone path. It needs no intent or Linear project. Attach unplanned work to an active project only when it blocks that project's stop criteria; otherwise keep it team-level. Preserve its source link or reference in the first `Source:` line, including when it attaches to a project.
- For trivial work, let `plan` apply its own skip test. Skip only the plan artifact, not the approved requirements or verification. Example: when acceptance criteria already imply one clear change in one obvious place with no route worth recording, build from the spec alone.
- If the request is only to use a skill or project guide, stop at that request's deliverable. Do not create tracker objects to make it fit this example.

Entry is settled when the user can see the chosen destination, the source requirement, and whether the requested work needs an intent, a spec, or only the directly requested skill output.

## Example policy: events and gates

Every row is conditional on the named event and the user's authorization for its writes. State names are this example's chosen mapping, not claims about every Linear team. If the bound team uses other names, adapt the mapping here before writing; do not silently select a near match. Keep project-specific identity and constraints in the Linear guide.

| Event | Action and destination | Observable completion |
|---|---|---|
| Work arrives without an approved spec | Size it using the entry rules. If capture is authorized, create a team-level issue or a placeholder in the selected project at `Backlog`; use the finite-effort path below when it needs an intent. Otherwise return the proposed destination in chat. | The captured issue exists at `Backlog`, or the user has the proposed destination and no tracker write occurred. |
| A finite effort has an approved intent | With file and Git publication permission, write `agent-docs/intents/<slug>.md` and land it on the default branch. With Linear permission, create the bound team's project at `planned`, using the intent's title as its name and the Goal's first sentence as its short description. Link the landed file from the overview and apply the guide's initiative choice. | The landed intent is reachable, the project is `planned`, and its overview link opens that file. Resolve placement with the user before creation if the guide does not settle it. |
| An intent is ready to slice or re-slice | Use `spec` to present the breakdown, then the completed specs for approval. With publication permission, put approved specs in issue descriptions at `Todo` under the project; publish coarse placeholders at `Backlog`. Omit the intent-backed `Source:` line when the project association carries that source. Create confirmed blocking relations after publishing blockers. | Every approved frontier slice has one issue at `Todo`, every remaining placeholder is at `Backlog`, and the native relations express the blocking order. |
| A standalone requirement is approved | Use `spec`'s standalone path, obtain approval of the completed spec, then publish on the user's word. Put it in the bound team's issue description, retaining the first `Source:` line. Use no project unless the entry rule attaches it to an active effort. | The approved spec exists at `Todo`, its source is identifiable, and its project association or absence follows the stop-criteria rule. |
| An approved issue is picked up | Read the issue and confirm its blockers are done or absent. Use `plan` to produce the route or state why it is trivial. With publication permission, attach the finished plan as a Document titled `Plan`. On authorized pickup, freeze the spec and any plan, move the issue to `In Progress`, and move its project to `started` if this is the first pickup. | The issue is `In Progress`, the plan Document is attached or the skip decision is reported, and any first-pickup project is `started`. Planning alone does not start implementation. |
| Implementation is requested | Build the approved spec in the checkout and branch selected under the Git guide. Follow the plan if one exists, and verify every acceptance criterion. Keep the issue `In Progress` through building and review. | The requested implementation exists in the checkout and observed verification addresses every criterion; unmet criteria and blockers are reported rather than marked done. |
| A PR is requested | Use `pr` to prepare the title and body from the actual change, requirement, and evidence. With publication permission, open one PR for one issue on the repository's PR host. Follow the Git guide for branch and review policy. | The PR exists at its reported URL and contains the skill's required record and observed evidence. The issue remains `In Progress`; opening a PR is not merge authorization. |
| The PR has merged | Confirm the merged PR and merge commit. With Linear permission, post a close-out comment on its issue identifying the PR and merge commit; add a sentence if delivery diverged from the spec. Move that issue to `Done`. Keep change-specific rationale in the PR and link lasting rationale in design-decision records. | The comment identifies the shipped change and the issue is `Done`; a merely open, closed-unmerged, or approved PR does not satisfy this event. |
| Work is dropped, superseded, or absorbed by a re-slice | On the user's word, move the affected issue to `Canceled`, or `Duplicate` when another issue already covers it. Point to the replacement when one exists and revise affected blocking relations. | The issue is terminal, any replacement is identifiable, and no dependent retains a misleading relation to the discarded slice. |
| All project issues are terminal and the intent's stop criteria appear met | Report the evidence and ask the operator whether to complete the project. On approval and authorization for all writes, move the intent to `agent-docs/archive/<slug>.md` and land that move on the default branch; then repoint the project overview to the archived file; then set the project to `completed`. | The archived file is landed, the overview link opens it, and the project is `completed`. Terminal issues alone never authorize completion. |

Perform tracker transitions explicitly at their events, using the `linear` skill's issue-update mechanism rather than branch-starting commands or integration-triggered closure. The `pr` skill's issue reference does not request automatic closure. Issue creation includes one type label and a priority under the project guide's constraints. Example defaults, if adopted and available in the bound team, are `Bug`, `Feature`, `Improvement`, `Chore`, or `Audit`; priorities are 1 urgent, 2 high, 3 medium as the default, and 4 low. Resolve conflicts with the guide before creating the issue.

## Example policy: revisions and frozen records

Before pickup, specs are malleable under `spec`. Re-slice into top-level issues rather than subtask trees. When the frontier reaches a placeholder larger than one session, re-scope that issue into the first real slice, create sibling issues, and re-examine every incoming blocking edge. An edge to the placeholder meant "blocked by all of it"; each dependent now needs the specific sibling or siblings that block it. With authorized publication, this revision is done when the approved frontier and the native relations agree and superseded issues have the terminal state described above.

An issue that outgrows one session goes through `intent` and the finite-effort event, with the original issue retained as its first spec. A project that collapses to one slice keeps its issue; on the user's word, detach that issue and cancel the redundant project. Preserve the intent file and its history unless the user authorizes a separate move. Either resizing path is done when the surviving issue, project association, and relations match the approved scope.

Each artifact freezes on its own clock. The intent settles once shaped and approved; later changes follow `intent`'s revision rules. The spec and plan freeze at pickup. A request to change frozen requirements returns to the user for a scope decision and the owning skill, not an implementation-time rewrite. The PR becomes the permanent record of the shipped change at merge; design-decision records follow the shared decision-record guidance.

When the route changes after pickup, leave the plan Document unchanged and record the divergence in the PR's Decisions section. When an approach is dead, use `plan` to prepare a replacement; with write authorization, attach the next numbered plan Document to the same issue and keep all earlier plans. Record why the approach failed in the PR's Decisions section, linking any lasting rationale in a design-decision record. The replacement is ready when it passes `plan`'s completion test and its new Document is attached; a route change does not silently change the spec or move tracker state.
