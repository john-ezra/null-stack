---
name: spec
description: Write specs from an intent or an approved standalone report or requirement. Use when an intent is ready to slice or re-slice as work lands, an approved bug report, GitHub issue, or explicit requirement needs a spec, specs need splitting, merging, re-scoping, or killing before pickup, or picked-up requirements need a scope decision.
disable-model-invocation: false
---

Write thin, session-sized **specs** from an intent or an approved standalone source: what each slice delivers plus its acceptance criteria, nothing more. How a slice gets built is not decided here.

For a spec already picked up, use [After pickup](#after-pickup) instead of re-slicing its approved contract in place.

## 1. Ground in the source

For intent-backed work, read the intent, especially Stop criteria, Constraints & decided, Out of scope, and Open questions. Then survey the existing specs and what blocks what, to see what is done, in progress, or already specced.

For standalone work, read the bug report, GitHub issue, or explicit requirement. Establish the expected result, constraints, exclusions, and unresolved questions from that source and the relevant existing work. Use the user's approval when already explicit; otherwise confirm the source requirement with them before slicing. A standalone spec needs neither an intent nor a project.

Done when the source is identified, its requirements are clear enough to slice, and you can name the **frontier**: the work whose blockers are done or absent.

## 2. Slice the frontier

Cut the frontier into **vertical slices**: each spec delivers a narrow but complete, independently verifiable path through the work, never a horizontal layer ("all the models", "all the endpoints") that proves nothing on its own. Size each slice to one session: one agent can plan, build, and verify it without a handoff. One task per slice: if the title needs an "and", it is two slices.

Decomposition is progressive. Slice finely only at the frontier; leave work behind unfinished blockers as coarse placeholders, a title and a sentence, until the frontier reaches it. An open question in the source blocks the same way: work that depends on its answer stays a placeholder, and the question is answered when the frontier reaches it, not before. Returning to re-slice as work lands is the mechanism working, not a planning failure. Until a spec is picked up, it is malleable: split, merge, re-scope, or kill freely.

Done when every piece of the frontier sits in exactly one slice, each slice is vertical and session-sized, and everything behind an unfinished blocker is a placeholder.

## 3. Get approval

Present the proposed breakdown to the user. Per spec: **title · what blocks it · what it delivers**. Iterate, splitting, merging, re-scoping, or killing, until the user approves the set.

## 4. Write the specs

### Source provenance

Keep a `Source:` link or reference in the spec body by default. Standalone reports and requirements always keep that reference, even when the spec belongs to a project.

Only intent-backed work under a workflow explicitly selected by the user may omit the line, and only when that workflow carries the source through the spec's project association. Before omitting it, follow that association to the intent and confirm it resolves to the intent used for the spec. Without a selected workflow or a confirmed association, keep the explicit `Source:` reference.

### Template

Spec template:

```markdown
# <What this slice delivers, in one imperative sentence>

Source: <link or reference to the intent or approved standalone report or requirement>

## Delivers

<What exists and works when this slice is done: the observable result, 1 to 3 sentences.>

## Acceptance criteria

- <Checkable condition an implementer can verify.>
- <...>
```

Present the completed specs for approval, including their acceptance criteria. Done when every approved frontier slice has a user-approved spec from the template, its source is explicit or confirmed under the rule above, every placeholder is still a title and a sentence, and the blocking order between them is stated once, outside the spec bodies. A spec body is the requirements contract for one slice; ordering does not belong in it.

## After pickup

Pickup freezes the approved requirements. Only a user scope decision can change them; implementation difficulty or a changed plan cannot.

1. Read the approved spec, its source, and any earlier amendments. Name the affected deliverables and acceptance criteria, the proposed change, and its cause. If only the route changes, leave the spec alone and use `plan` for the route. If the proposal changes the source intent or requirement, settle that source change with the user too. Done when the difference between the approved contract and the proposal is explicit.
2. Get the user's scope decision: retain the contract, amend the same slice, or replace it with different slices. Use an already explicit decision; otherwise present the proposal and wait. If the user declines or has not decided, keep the contract unchanged and report any criterion that cannot be met. Retaining the contract may include separately approved follow-on work, but moving an unmet original criterion into follow-on work requires an amendment or replacement. Done when the user has chosen the disposition.
3. Prepare the chosen record:
   - **Amend the same slice.** The amended slice must remain vertical and session-sized. Leave the original approved body and earlier amendments intact. Append `Amendment 1`, then `Amendment 2`, with a date, the reason, an explicit reference to the change's source, and the user's approval reference. State each added, removed, or replaced requirement, including the exact before-and-after wording for changes to existing deliverables or criteria. Unmentioned requirements still apply; later amendments override only the changes they name.
   - **Replace the slice.** Write replacement specs through the grounding, slicing, and approval sections above. Keep the original approved body and amendments, adding a dated supersession note that references the replacements, change source, and user approval. Each replacement references its predecessor and the change source. Keep the old requirements readable rather than overwriting them with the new slices.
   - **Keep the contract and add follow-on work.** Leave the original spec unchanged. Write the separately approved work through the grounding, slicing, and approval sections above, referencing the original spec and the new requirement. The original still owes every acceptance criterion; state any blocking order outside the spec bodies.
4. Present the completed amendment or new specs for approval, including all changed acceptance criteria. Use approval already explicit for that exact content; otherwise wait. Record the date and a reference to that approval with the change source in the amendment or new specs. Content approval grants no file or tracker-write permission. Without that permission, return the proposed records in the conversation; with it, write only to the authorized destination. Done when the approved effective contract, original requirements, change source, and new approval are identifiable, and the records are either delivered in chat or written as authorized.

Keep existing plans frozen. Reassess the route against the approved contract through `plan`; a workflow, if selected, owns plan placement and replacement, spec publication, relations, and tracker states. A scope decision alone authorizes none of those writes.
