# Development policy
---
This file is the project's lifecycle policy. Skills own their procedures and artifact formats; this guide owns entry thresholds, artifact homes, approval and write rules, tracker mapping, and completion. Reading it authorizes no execution or publication.

*This template becomes `agent-docs/DEVELOPMENT.md`; its links resolve from there. Fill each section with explicit project choices, or replace the whole file with the no-lifecycle block at the end. Project Starter's `agent-docs/DEVELOPMENT.md` is a filled example of this document, a finite-effort policy with Linear. Confirm every choice before adopting it; copying an example does not adopt it.*

*Keep Git choices in [GIT.md](GIT.md), Linear bindings in [LINEAR.md](LINEAR.md), and lasting-decision rules in [design-decisions/README.md](design-decisions/README.md). Resolve conflicts with [project write restrictions](../AGENTS.md#rules) rather than repeating or weakening them. Delete the editing instructions and examples when filled. The finished guide is usually 400-700 words; policy complexity, not a word quota, decides.*

*Open with the selected workflows, if any, and the rule for running them.*

```
Example: This policy selects the finite-effort lifecycle below and one task workflow, [fix-bug](../workflows/fix-bug/SKILL.md). Run a workflow only on explicit request. Apply only the requested event; finishing one does not authorize the next.
```

## Development paths

*Say how a request chooses its path and what each path requires before implementation. Name the threshold for written scope: which changes need a spec, which need an intent, and when a plan is required. Say whether the user may override the default path.*

```
Example: Routine maintenance (corrections, repairs, bounded improvements) proceeds from the request to implementation. Substantive changes (new capabilities, permission or ownership changes, contract changes) need approved written scope first: a standalone spec for one verifiable outcome, or an intent plus specs when several changes serve one goal. Plan when the route needs it. The user may override either way.
```

## Tracker

*Say what the tracker owns and how work enters it. Map artifacts to records, such as an issue per spec and a project per intent, and say which work needs no record. If the project does not use a tracker, say so and remove this section; do not invent bindings to fill it. Keep identities and constraints in [LINEAR.md](LINEAR.md).*

```
Example: Linear owns intake, status, and blocking relationships. One issue per standalone spec; one finite project per intent, with an issue per spec. Routine maintenance needs no new record.
```

## Artifact homes

*Give the authoritative home for each artifact the policy uses, including where inactive artifacts go and how their outcome is recorded. Say whether tracker records link to files or hold copies.*

```
Example:

| Artifact | Active directory | Archive directory |
|---|---|---|
| Intent | `agent-docs/ephemera/intents/` | `agent-docs/ephemera/archive/<outcome>/intents/` |
| Spec | `agent-docs/ephemera/specs/` | `agent-docs/ephemera/archive/<outcome>/specs/` |
| Plan | `agent-docs/ephemera/plans/` | `agent-docs/ephemera/archive/<outcome>/plans/` |

Outcomes are completed, canceled, or superseded. Linear records link to these files rather than hold copies.
```

## Verification

*Match required evidence to kinds of change. Say when a temporary check suffices and when a permanent regression check is warranted.*

```
Example: Mechanical edits need a review of the changed content and its links. Behavior changes need the specific test or scenario that covers them, plus a nearby case where the new behavior should not apply. Keep checks temporary unless one guards a specific plausible failure.
```

## Closeout

*State when an issue is complete, when an effort is complete, and the order of archival, publication, link updates, and tracker transitions. A merged change with unmet acceptance criteria does not complete the issue.*

```
Example: An issue closes when its acceptance criteria are verified and any required merge has succeeded. Archive the spec and its plans, publish that change, update the Linear links, then apply the authorized state change. An effort closes when its intent's stop criteria are met, every issue is resolved, and the user approves after seeing the evidence.
```

## Existing boundaries

*Point to the guides this policy defers to. Keep only pointers here.*

```
Example: Follow [project write restrictions](../AGENTS.md#rules) and [Linear write permission](LINEAR.md#linear-write-permission). Before Git or PR work, read [Git conventions](GIT.md). Before designing, changing, or reviewing an area, read [design decisions](design-decisions/README.md).
```

## Option: no lifecycle

*Replace the entire file with this block, without its outer fence, if the project chooses no lifecycle.*

```markdown
# Development policy

No development lifecycle is selected for this project. Use only the requested skill or project guide; do not infer tracker records, artifact homes, or task transitions. Resolve any destination or permission needed for that request before writing. Reading this guide does not authorize execution or publication.

Before Git or PR work, read [Git conventions](GIT.md). Before Linear access, read [Linear context](LINEAR.md). Before design, change, review, or decision-record maintenance, read [design decisions](design-decisions/README.md). [Project write restrictions](../AGENTS.md#rules) still apply.
```
