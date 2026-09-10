# Design decisions

Use this guide to read, write, or revise a lasting design decision. This is support material, not a request to run a full design review. Project guidance chooses the record's repository and path. When it also supplies record selection, format, or maintenance rules, use those project-owned rules instead of the corresponding defaults below. A workflow may refer to that home but is not required.

## What earns a record

Record a choice when future work needs its reasoning after the originating task ends. Architecture, ownership boundaries, persistence, compatibility, and consequential rejected alternatives can qualify. In a toolkit or documentation project, this includes the design of resources and their responsibilities.

Keep goals and work-scoping choices in the intent or requirements, implementation steps in the plan, and change-specific rationale in the PR. Routine implementation choices need no separate record. Plans and PRs link lasting rationale rather than copy it.

## Read and maintain

1. Before designing, changing, or reviewing an area, use the project's decision guide to locate records and read the relevant ones, including their reconsideration conditions and any replacements. Read the affected source too. This is done when the current decisions that constrain the work and any conflict with present evidence are identified; the guide alone is not the record.
2. When a lasting choice emerges during shaping, planning, or implementation, distinguish an accepted decision from a recommendation. An unapproved recommendation stays a proposal. Write only when the user's request authorizes the record's file changes; agreement with the choice alone does not grant that permission. Otherwise present the proposal and its intended home in chat. Neither path requires a tracker transition or a separate lifecycle stage.
3. Before writing, read the existing record if there is one and the evidence for the choice. Use one record per decision, a descriptive uppercase, hyphen-separated `<SLUG>.md` without sequence numbers, and a date inside. Do not reconstruct motivation from today's structure. For a backfill, cite maintained evidence, identify the date as the recording date when the original decision date is unknown, and state any gap rather than inventing an account.
4. Write the accepted choice using the format below. Give each rationale one authoritative home and link its sources. Keep private information out of public records; a public record must make sense without private access. Finish when the decision, reasons, meaningful alternatives, consequences, and reconsideration conditions are explicit and supported. A record without a defensible reason is not ready.
5. When evidence challenges a decision, surface the conflict rather than silently following it or bypassing it. Propose the change to the user. With approval and file-write permission, revise the same record and add a dated revision explaining what changed and why. Preserve earlier reasoning in the revision history and Git history. If a distinct decision supersedes it, retain the old file, mark it superseded with a link to the replacement, and link back from the replacement. Update affected guidance and references in the same change; a revised decision is not permission to change code or publish it.

## Record format

Replace the angle-bracket instructions. Keep the posture in each record. Add a Revisions section when the decision changes, not an empty section at creation.

```markdown
# <Decision title>

Date: <YYYY-MM-DD; label as recording date if the original decision date is unknown>

> Current best understanding, held for the recorded reasons. A better argument wins: update the record, don't route around it. Never silently obey a stale decision; never silently ignore a live one.

## Context

<The problem and constraints that made the choice necessary. Link the evidence or source requirements; distinguish known facts from uncertain history.>

## Decision

<The accepted choice and the area it governs.>

## Reasons and alternatives

<Why this choice fits the constraints, and why meaningful alternatives were rejected. Omit alternatives that were never considered rather than inventing a comparison.>

## Consequences

<What future work must preserve, what this enables, and the costs or tradeoffs accepted.>

## Reconsider when

<Concrete changes in constraints or evidence that would justify reopening the decision.>
```
