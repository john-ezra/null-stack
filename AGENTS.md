# Null Stack

A collection of agent skills, shared workflows, and project starter templates. This file governs maintenance of the collection; it is not the project `AGENTS.md` template.

## Read when needed

| Work | Guidance |
| --- | --- |
| Write or review a skill, workflow, template, or other agent-facing instruction | [agent-prose](Skills/agent-prose/SKILL.md), following its pointers for the selected task |
| Change resource ownership, layout, project-template scope, packaging, frontmatter, resource links, or discovery | [Packaging](Skills/agent-prose/PACKAGING.md); read its OMP support when host behavior matters |
| Write or revise prose | [natural-english](Skills/natural-english/SKILL.md) |
| Set up the collection, copy a starter, or share resources | [README](README.md) |

## Boundaries

`Templates/` contains editable source material, not instructions governing work in this repository. The project template's embedded rules apply to a consuming project after customization, not to maintaining that template here.

Keep skill support files inside their owning package. Preserve the existing skills and shared lifecycle unless the requested change requires an edit. Project guidance must remain usable without adopting a workflow, and workflows remain manually invoked.

Keep reusable resources self-contained within this checkout. Put project-specific tracker bindings and instructions in the consuming project; use labeled examples rather than actual workspace, team, or initiative bindings here.

Update links in the same change that moves their targets. For a changed starter, verify its links after copying it outside this repository; repository-relative success alone is insufficient.

Commit or push only on explicit request. Changing this collection does not authorize installing resources, modifying live agent configuration, or overwriting a consuming project's guidance.
