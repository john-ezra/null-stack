# Development policy

This policy selects the finite-effort lifecycle below and two task workflows, [fix-bug](../workflows/fix-bug/SKILL.md) and [add-feature](../workflows/add-feature/SKILL.md). Run a workflow only on explicit request. Apply only the requested event; finishing one does not authorize the next, and reading this guide authorizes no execution or publication.

## Development paths

Choose the path by the scope and impact of the change, not the number of lines changed. The user may override it for the requested work, either proceeding directly to implementation or choosing the fuller process.

### Routine maintenance

Corrections, repairs, and incremental improvements to existing behavior, where the desired outcome is clear and the effect stays within an existing component's responsibilities. Proceed from the request to implementation and verification without an intent, spec, or plan, within the permissions already granted.

### Substantive changes

New capabilities, changes to permission or privacy boundaries, changes to ownership or responsibilities, and changes to contracts other code relies on. Establish approved written scope before implementation.

Use a standalone spec when the request describes one self-contained, independently verifiable outcome. Use an intent when several deliverable changes serve a larger goal; it holds their shared purpose, constraints, and stop criteria, and specs divide the effort into implementable pieces. Importance or risk alone does not require an intent. Plan when the implementation route needs it, not as a compulsory document.

Use the owning skill for each artifact. `intent`, `spec`, and `plan` own their contents and revision rules; this guide owns policy and destinations.

## Linear-first work

Linear owns intake, issue and project status, and blocking relationships. Work normally starts from an existing record: develop an issue's requirement into a spec, or a project's goal into an intent. Use one issue per standalone spec and one finite project per intent, with an issue for each of its specs. Routine maintenance needs no new record; when the user selects an existing issue, keep the work attached to it.

When work starts in a session and needs a spec or intent, create the issue or project from that session under [Linear write permission](LINEAR.md#linear-write-permission). Session-originated and Linear-originated work use the same mapping.

## Artifact homes

The workspace repository holds the authoritative intent, spec, and plan files. Linear records link to those files rather than hold copies of their bodies: link an intent from its project, and a spec and its plans from their issue. Implementation may proceed against approved local artifacts; publishing them is not a prerequisite. Add or update Linear links only after their targets are published.

| Artifact | Active directory | Archive directory |
|---|---|---|
| Intent | `agent-docs/ephemera/intents/` | `agent-docs/ephemera/archive/<outcome>/intents/` |
| Spec | `agent-docs/ephemera/specs/` | `agent-docs/ephemera/archive/<outcome>/specs/` |
| Plan | `agent-docs/ephemera/plans/` | `agent-docs/ephemera/archive/<outcome>/plans/` |

The outcome is `completed` when the work met its completion criteria, `canceled` when it was deliberately stopped short of its scope, and `superseded` when another artifact or effort replaced it. Preserve the reason for cancellation or supersession and links to any replacement. Do not rewrite unfinished requirements to imply they were met.

For an explicitly requested session handoff, use `handoff` and write the file in `agent-docs/ephemera/handoffs/`.

## Verification

Match the proof to what changed:

| Change | Required evidence |
|---|---|
| Mechanical edits | Review the changed content and check affected links. |
| Behavior changes | Run the specific test, command, or scenario that covers the change, including a nearby case where the new behavior should not apply. |
| Agent-facing instructions | Exercise representative requests. When the wording's effect is uncertain, use a blind comparison. |

Keep checks temporary by default. Retain a permanent regression check only when it protects against a specific plausible failure. Report what was exercised, the observed results, and any remaining verification gaps.

## Closeout

An issue closes when its acceptance criteria are verified and any required merge or publication has succeeded. A merged PR with unmet criteria does not complete the issue.

Before project closeout, confirm all three conditions: the intent's stop criteria are demonstrably met; every associated issue is resolved, accounting for canceled and superseded issues without treating them as delivered work; and the user has approved completion after seeing the evidence.

Archive a spec and its plans at issue closeout and the intent at project closeout. Completed issue artifacts do not wait for the rest of their project. For an authorized closeout:

1. Move the artifacts to their archive directories and repair affected repository links in the same change.
2. Publish that repository change.
3. Update the corresponding Linear links to the archived paths and verify they resolve.
4. Apply only the authorized Linear state change, using the actual outcome rather than treating canceled or superseded work as completed.

Closeout is incomplete while publication, link updates, or verification remain outstanding. Use `pr` for merge evidence and closeout records. After closeout succeeds, follow [branch cleanup](GIT.md#branch-cleanup) and report any cleanup left pending.

## Existing boundaries

Both paths follow [project write restrictions](../AGENTS.md#rules) and [Linear write permission](LINEAR.md#linear-write-permission). Before Git or PR work, read [Git conventions](GIT.md). Before designing, changing, or reviewing an area, read [design decisions](design-decisions/README.md).
