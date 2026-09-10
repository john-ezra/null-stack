---
name: intent
description: Write an intent document. Use when the user wants an idea, want, or problem captured as an intent, asks for an INTENT.md, or needs an existing intent updated.
disable-model-invocation: false
---

Use this skill when the user wants an idea, want, or problem captured as an intent, asks for an INTENT.md, or needs an existing intent updated. Write what is wanted, why, and under which constraints, in the originator's own words. Use what the conversation has already produced. Add nothing of your own: no solutions, no design, no restructuring of the want. Where the conversation has not settled something, say so under Open questions rather than filling the gap.

Goal is the one section that cannot be open: without a stated want there is nothing to write, so ask for it before drafting. Every other section may be open at creation. Write what the conversation holds and stop; a thin intent is a valid intent, and its open questions are filled later, not by interview here.

Template, verbatim:

```markdown
# <Name of the effort>

## Goal
<What is wanted, and why.>

## Stop criteria
<The checkable definition of done for the whole effort.>

## Constraints & decided
<Hard requirements and decisions already made.>

## Out of scope
<Explicitly not this work.>

## Open questions
<Explicitly unresolved. Permission to not know yet.>
```

Include every section; make a genuinely empty one say so rather than vanish.

Present the draft for correction. Done when the originator has approved it and it reads as their want. Approval does not grant file or tracker-write permission. Use the destination authorized by the request or adopted project policy; otherwise return the approved draft in chat. An intent needs no workflow or tracker.

## Revision

Answering an open question is routine: move it from Open questions to the section it settles, the moment it is answered. Changing the approved want itself (Goal, Stop criteria, a constraint) is rare and needs a serious cause: new facts, a collapsed assumption. Implementation drift is not one; the intent holds and the work bends. Get the originator's approval for the changed want, using an already explicit decision when available. With write permission, update the affected sections in place; otherwise present the revision in chat. Approval of the revision does not authorize downstream spec changes or publication.
