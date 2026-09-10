---
name: plan
description: Implementation planning. Use when converting a spec into an implementation plan, picking up specced work, deciding whether a spec needs a plan, or reassessing or replacing an approach after pickup.
disable-model-invocation: false
---

Convert a spec into the literal implementation plan: a frozen snapshot of *how*, taken at pickup, after all decisions are made. The spec stays the requirements contract; the plan is the route. Non-goals: writing or re-scoping the spec, and implementing.

For a route change after pickup, use [After pickup](#after-pickup). Plan placement comes from the user's request or adopted project policy, not from a workflow requirement. Without a destination or write permission, deliver the plan in chat. Planning does not authorize implementation or tracker changes.

## When to skip

Trivial work runs off the spec alone. Trivial means the spec's acceptance criteria already imply the obvious implementation: one clear change, one obvious place, no ordering or risk worth writing down. If you would restate the spec in different words, skip the plan. Skipping the artifact leaves the approved requirements and their verification unchanged. Done deciding when you can say which side the spec falls on and why.

## Steps

1. **Read the spec.** Take in what it delivers, its acceptance criteria, and what blocks it. Read the code the change touches and the relevant design decisions through the project's decision guide. Resolve every open decision now: look up what the environment can answer, put every judgment call to the user. The plan comes after decisions, not to defer them. When this settles a lasting design choice, follow [decision-record guidance](skill://software-design/DECISIONS.md) and the project's record home within the user's write authorization. Link the record from the plan rather than duplicate its rationale.

2. **Draft the plan** using the template below. Fill every section with specifics: real file paths, real commands, real expected outputs. For destinations with separately titled records, name the initial record `Plan`.

3. **Interrogate the draft before accepting it.** Answer in the plan itself, not in your head:
   - What could this break?
   - Which step is riskiest, and what is the fallback if it fails?
   - Which approaches were rejected, and why?

   Then apply the completion test: **an agent that has never seen this conversation could implement the spec from the plan alone.** If any step needs the conversation to make sense, the plan is not done.

## Template

```markdown
# Plan: <spec title>

## Files that change
<each file touched, what changes in it; files created, and why>

## Order of work
<numbered steps, in dependency order>

## Risks
<what this could break; the riskiest step and its fallback; approaches rejected and why>

## Proof
<one check per acceptance criterion in the spec, quantifiable: which test passes, what the screenshot matches, what the endpoint returns>
```

## After pickup

1. Read the approved spec, its amendments, the current plan if one exists, and the evidence that the route changed. If the proposal changes deliverables or acceptance criteria, use `spec` for a scope decision before planning against that change. Done when the effective requirements and the reason for reassessing the route are explicit.
2. Keep every picked-up plan unchanged. For a divergence within a viable approach, report the changed route and its reason without rewriting the snapshot. If the approach is abandoned, prepare a complete replacement through the steps above, including why the earlier approach failed and a reference to it. If no plan exists, apply the ordinary planning steps. Apply the skip rule when the remaining work needs no plan, without deleting an earlier record.
3. If recording a replacement, number it `Plan 2`, `Plan 3`, and so on after the initial plan. Inspect existing records for this spec and take the number after the highest existing one; keep all predecessors. Use the same spec association and the authorized artifact home. For Linear Documents, use `linear` to create and confirm a new attachment, not to overwrite the old Document. Other destinations use the same preserved sequence without requiring Linear.
4. Report the selected route or replacement and any outstanding write. A failed publication does not make the new plan authoritative. When the work has a PR, use `pr` to record route divergence and abandoned approaches in Decisions, linking lasting rationale through the project's decision guide. Done when a successor can identify the effective route, its requirements, and every earlier plan without inferring a scope or state change.
