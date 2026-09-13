# Project Starter
---

A reference layout for a private project workspace with the code in a separate Git repository. Use it to assemble the templates into guidance that fits your project. This document explains the layout; it is not a filled project policy or a file the agent needs during ordinary work.

## Workspace layout

```text
<project>-workspace/
  .gitignore
  .gitmodules
  AGENTS.md
  agent-docs/
    PROJECT-OUTLINE.md
    DEVELOPMENT.md
    GIT.md
    CODE-STYLE.md
    LINEAR.md                  # optional
    research/
      README.md
    design-decisions/
      README.md
  workflows/                   # optional
    <task>/
      SKILL.md
  .worktrees/                  # ignored, created when needed
  <project>/                   # code repository, a Git submodule
```

The workspace keeps agent guidance and project administration in a private repository. The code submodule has its own history and pull requests and can be public or private. This separation lets you change how agents work without putting that guidance in the code repository. The workspace records the code revision it uses through Git's submodule pointer.

This is a suggested arrangement, not a requirement for using the templates or skills. A single repository can hold both code and guidance. If you choose that arrangement, omit the submodule and adapt the repository descriptions and paths accordingly.

## Document map

Source links below open the templates in this directory. Destination paths are relative to the consuming workspace root.

| Template | Destination | Responsibility |
| --- | --- | --- |
| [AGENTS.md](AGENTS.md) | `AGENTS.md` | Short project overview, commands, structure, ambient rules, and pointers telling an agent when to read each guide |
| [PROJECT-OUTLINE.md](PROJECT-OUTLINE.md) | `agent-docs/PROJECT-OUTLINE.md` | The project's purpose, audience, capabilities, and broad scope, separate from individual tasks |
| [DEVELOPMENT.md](DEVELOPMENT.md) | `agent-docs/DEVELOPMENT.md` | The chosen lifecycle or explicit no-lifecycle policy, artifact homes, verification, and completion rules |
| [GIT.md](GIT.md) | `agent-docs/GIT.md` | Repository ownership, publication permission, branches, commits, reviews, merges, and worktrees |
| [CODE-STYLE.md](CODE-STYLE.md) | `agent-docs/CODE-STYLE.md` | Code and prose conventions, with pointers to the project's actual tooling |
| [LINEAR.md](LINEAR.md) | `agent-docs/LINEAR.md` | Confirmed Linear bindings, tracker-write permission, and project constraints, if Linear is used |
| [RESEARCH.md](RESEARCH.md) | `agent-docs/research/README.md` | Where research reports go and when to consult them; findings and recommendations remain distinct from approved decisions |
| [DESIGN-DECISIONS.md](DESIGN-DECISIONS.md) | `agent-docs/design-decisions/README.md` | How to select, record, approve, and revise lasting decisions; the records live beside this guide |
| [WORKFLOW.md](WORKFLOW.md) | `workflows/<task>/SKILL.md` | A chosen skill sequence for a recurring task; extract and customize the template block rather than copying the whole authoring document |

Keep the overview short and put each policy in its own guide. For example, the overview points to the development policy rather than repeating its lifecycle. Research holds evidence; design-decision records hold accepted choices and their reasons. Task-specific requirements and plans belong at the artifact homes the project selects in its development policy, not in the project outline.

Reusable skills supply task procedures. A project workflow names the skills to use and their order without copying those procedures or the project's policy. Neither adopting a guide nor writing a workflow runs it.

## Choose what applies

The layout does not select a tracker, lifecycle, branch scheme, merge method, or workflow. Fill those choices in their owning guides. Existing examples show possible answers; they do not become project rules until you adopt them.

- **Without Linear.** Omit `agent-docs/LINEAR.md`. Remove its row and tracker rule from `AGENTS.md`, and remove or replace Linear references in the development policy and any other retained document. If you use another tracker, give its bindings and permissions a project-owned home and update the pointers to match. Do not invent a tracker account to fill a template.
- **Without workflows.** Omit `workflows/`, state that none are selected in the overview and development policy, and remove workflow links and instructions that assume a workflow exists. Individual skills remain usable on their own.
- **Without a lifecycle.** Use the no-lifecycle block in [DEVELOPMENT.md](DEVELOPMENT.md#option-no-lifecycle), adapted to the project. Keep the resulting policy file so overview and optional workflow pointers have a real destination. A workflow does not require adopting a lifecycle.

## Assemble the workspace

1. Choose the repository arrangement and document ownership before copying files. For an existing project, reconcile its guidance rather than overwriting it with these templates.
2. If using the two-repository layout, create the private workspace repository and add the existing code repository as its submodule. Git creates or updates `.gitmodules` and records the submodule pointer; neither comes from a Markdown template. Record both repositories and their publication order in `agent-docs/GIT.md`.
3. Create the directories and copy the selected templates to the destinations in the document map. Create `.gitignore` yourself, preserving existing entries. For the illustrated worktree location, add `/.worktrees/`; create worktrees there only when needed under the project's Git conventions. Keep a copy of the toolkit's [license](../license) with adopted material without replacing either repository's own license.
4. Follow each template's authoring instructions. Replace annotations with confirmed project facts, remove unused examples and editing notes, and retain useful project rules and document formats. Template links resolve from their destination paths, not from this directory. The research and design-decision guides already contain generic rules; adapt them only where the project differs and remove their authoring notes.
5. For each workflow you choose, follow [WORKFLOW.md](WORKFLOW.md) to create its `SKILL.md`. Add overview and policy links only after the workflow exists. Make its required skills available separately through your harness; templates are not a skill-discovery root, and workflows remain manually invoked.
6. Check the assembled workspace outside the toolkit checkout. Every retained local link and anchor must resolve, including workflow-to-policy links. Check that omitted tools or workflows have no remaining references and that ordinary project guidance requires no access to the toolkit checkout. Start agent sessions at the workspace root so they load its `AGENTS.md`.

The adopted files belong to the consuming project. Updating Null Stack does not overwrite its choices.
