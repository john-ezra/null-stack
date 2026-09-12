# Null Stack

A collection of agent skills, the copy-ready Project Starter, and authoring templates. Use a skill on its own, adopt the starter's defaults, or assemble project guidance and workflows to suit your work.

## What lives here

| Location | Purpose |
| --- | --- |
| [skills/](skills/) | Standalone capabilities, with a root `SKILL.md` and supporting documents under each skill's `resources/` directory |
| [project-starter/](project-starter/) | Opinionated, copy-ready guidance for a private workspace that holds the project's code as a Git submodule, with a finite-effort lifecycle, Linear conventions, and two task workflows; project-specific facts stay empty |
| [templates/AGENTS.md](templates/AGENTS.md) | Project overview template with section instructions, examples, the guide table, rules, and how-to-use steps; becomes the project's `AGENTS.md` |
| [templates/PROJECT-OUTLINE.md](templates/PROJECT-OUTLINE.md) | Template for the project's purpose, audience, capabilities, and scope; becomes `agent-docs/PROJECT-OUTLINE.md` |
| [templates/CODE-STYLE.md](templates/CODE-STYLE.md) | Template for code conventions, documentation, naming, Markdown and prose, and formatting; becomes `agent-docs/CODE-STYLE.md` |
| [templates/DEVELOPMENT.md](templates/DEVELOPMENT.md) | Blank lifecycle policy with per-section instructions, examples, and a no-lifecycle option; becomes `agent-docs/DEVELOPMENT.md` |
| [templates/GIT.md](templates/GIT.md) | Template for repositories, branching, worktrees, commits, pull requests and merges, and branch cleanup; becomes `agent-docs/GIT.md` |
| [templates/LINEAR.md](templates/LINEAR.md) | Template for Linear bindings, write permission, and project constraints; becomes `agent-docs/LINEAR.md` |
| [templates/WORKFLOW.md](templates/WORKFLOW.md) | Authoring steps and one generic fenced block for a task workflow; the block becomes `workflows/<name>/SKILL.md` |

A reusable skill owns its task procedure and artifact semantics, including revision and close-out. Project lifecycle policy chooses entry thresholds, artifact destinations, project approval gates and write rules, tracker event mapping, and effort completion. Short task workflows select skills and their order without repeating procedures or policy. Topic guides own Git conventions, Linear bindings and constraints, and lasting design decisions; shared skill defaults defer to project-owned record rules. Copying the starter adopts its policy; copying a template adopts nothing until it is filled. Neither executes a workflow.

## Use the shared library

Keep one canonical checkout of `skills/` rather than copying it into every project. Changes to that checkout affect the projects using it. To distribute an individual skill, follow [Share individual skills](#share-individual-skills).

Make the library available through your harness using its current documentation for setup, discovery, and invocation. Null Stack maintains one source, without per-harness configuration recipes, adapters, or generated variants. Live setup or migration requires explicit permission and must preserve unrelated settings and resources. Do not expose `templates/` or the toolkit's `project-starter/` as runnable skills.

Preserve the common package layout when sharing the library:

```text
skills/
  <name>/
    SKILL.md
    resources/
      <supporting-file>.md
```

Keep required cross-package dependencies beside one another under `skills/`; packages without support need no `resources/` directory. Skills may also require task tools such as Git, a runnable project, or the Linear CLI, and some procedures require independent delegates. Report a missing capability rather than silently skipping a step or claiming completion. A missing capability is not permission to install it.

Each skill states its invocation policy in metadata and body prose. Listed skills may be selected when their stated conditions apply; being listed does not guarantee selection. Manual skills and generated workflows require an explicit user invocation through an entrypoint the harness supports. Some hosts require a native user command rather than an ordinary request to the agent. The harness supplies that command; Null Stack does not maintain a separate command definition. Reading source or support does not authorize execution.

The library's layout and prose do not establish runtime compatibility by themselves. Verify required reads, invocation behavior, and delegation in the harness and model version you use.

## Share individual skills

Share the skill with all its required dependencies, including those reached through other packages.

1. Start with the skill's `SKILL.md` and follow its supporting-file pointers. Read every supported branch, including conditional ones, and identify instructions that require another skill or resource. Check references by name as well as links. A required read or handoff counts even if your first task will not trigger it; an optional adjacent suggestion, such as `test-quality`'s `shakedown` suggestion on request, does not.
2. Add the complete owning package for each required destination, then inspect that package's instructions and support in the same way. Repeat until every required destination belongs to an included package and no unread required references remain. Visit each package once so references back to an included package do not loop.
3. Copy those package directories with all their supporting files and a copy of [license](license). Preserve package names and internal paths. Keep shared rules in their owning package, as [Shared material](skills/agent-prose/resources/SKILL-AUTHORING.md#shared-material) explains; do not paste a dependency's rules into the skill that uses them.
4. Make the copied packages discoverable through the destination host using its current documentation, then check every required read against the copied distribution with the original checkout and unrelated installed skills unavailable. Check both skill entry points and supporting-resource paths. Reading support does not invoke its owning skill, and installing the packages does not adopt a workflow.

For example, [software-design/resources/DEEPENING.md](skills/software-design/resources/DEEPENING.md) sends test-retirement decisions to the deletion gate in [test-quality/SKILL.md](skills/test-quality/SKILL.md#deletion-gate). Include the complete `software-design/` and `test-quality/` packages, including `test-quality/resources/ASSERTIONS.md` and `test-quality/resources/DOUBLES.md`. Keep the gate in `test-quality`; this README and the copied `software-design` package should only point to it. This is one required dependency path, not the end of the discovery procedure: follow the remaining required references before declaring the distribution complete.

## Start a project

Project Starter seeds a private workspace repository that holds the project's code as a Git submodule. The workspace keeps agent guidance, agent docs, workflows, tracker configuration, and worktrees, with its own history; the project repository keeps the code and its pull requests, with no agent material, and can be public or private.

Create the workspace repository and copy the contents of [project-starter/](project-starter/) into it, including the `.gitignore` and the entire `agent-docs/` and `workflows/` directories, without overwriting existing guidance. Then add the project repository as a submodule:

```sh
git submodule add <project-url> <project>
```

Preserve the toolkit's [license notice](#license) without replacing either repository's license. For an existing project, reconcile its current instructions before adopting the starter. Start agent sessions at the workspace root so the agent loads the workspace's `AGENTS.md`.

```text
<project>-workspace/
  .gitignore
  AGENTS.md
  agent-docs/
    PROJECT-OUTLINE.md
    GIT.md
    CODE-STYLE.md
    LINEAR.md
    DEVELOPMENT.md
    research/
      README.md
    design-decisions/
      README.md
  workflows/
    fix-bug/
      SKILL.md
    add-feature/
      SKILL.md
  <project>/
```

The starter's `AGENTS.md` keeps empty sections for the project name and purpose, tech stack, commands, and project structure. The [project outline](project-starter/agent-docs/PROJECT-OUTLINE.md) holds the fuller project description, with empty sections for purpose, audience, capabilities, and scope. Fill them with confirmed facts when customizing; leaving them empty does not block ordinary work. The operating defaults, guide pointers, and permission rules are already filled in. The [Git conventions](project-starter/agent-docs/GIT.md) select the two-repository layout and its publication order, kind-prefixed task branches, worktrees under `.worktrees/` at the workspace root, plain imperative commit subjects, squash merges that delete the task branch, and worktree cleanup after closeout; the [code style](project-starter/agent-docs/CODE-STYLE.md) follows the consuming repository's tooling and sets Markdown and prose rules; design-decision rules and format stay local. It selects the finite-effort lifecycle in [agent-docs/DEVELOPMENT.md](project-starter/agent-docs/DEVELOPMENT.md), keeps Linear conventions in [agent-docs/LINEAR.md](project-starter/agent-docs/LINEAR.md) with an empty bindings table for the project to fill, and ships two task workflows, [fix-bug](project-starter/workflows/fix-bug/SKILL.md) and [add-feature](project-starter/workflows/add-feature/SKILL.md), which run only on explicit request.

Keep research reports in [agent-docs/research/](project-starter/agent-docs/research/README.md). Its guide explains where to save reports and when to consult them. Research holds findings and supporting sources; accepted decisions and their rationale belong in `design-decisions/` under its guide's rules. The project outline stays separate from task-specific goals, requirements, and plans when those artifacts are used.

For help filling project-specific sections, read the instructions and examples in the [AGENTS.md template](templates/AGENTS.md). The instructions live in the template itself, not in a separate customization guide. The starter's pointer names the source path and uses the public template URL so it survives copying. Ordinary work needs no network access, toolkit checkout, installed skills, or host-specific resolver.

To adopt a different policy, use [templates/DEVELOPMENT.md](templates/DEVELOPMENT.md) to write the project's `agent-docs/DEVELOPMENT.md`, or replace the file with that template's no-lifecycle block. Keep only the adapted policy, without authoring instructions or outer fences, and adapt its links to the consuming project. Policy and task workflows are separate choices; a project that drops a shipped workflow also removes its links from the overview and the policy.

### Author a project AGENTS.md

Use [templates/AGENTS.md](templates/AGENTS.md) for the overview template. Templates are flat, one file per document kind, and each is a blank copy-source with inline editing instructions and examples that names its destination in the project. Copy `templates/AGENTS.md` as the project's `AGENTS.md`, and copy the companion templates, [PROJECT-OUTLINE.md](templates/PROJECT-OUTLINE.md), [DEVELOPMENT.md](templates/DEVELOPMENT.md), [GIT.md](templates/GIT.md), [CODE-STYLE.md](templates/CODE-STYLE.md), and [LINEAR.md](templates/LINEAR.md), into `agent-docs/`. The research and design-decision guides have no template; copy [research/README.md](project-starter/agent-docs/research/README.md) and [design-decisions/README.md](project-starter/agent-docs/design-decisions/README.md) from Project Starter, or remove their rows from the overview's table. Template links resolve from their destination in the consuming project, not from `templates/`. Follow the overview's "How to use this template" section to adapt it and the companion guides.

The templates are authoring material; `project-starter/` is the opinionated, ready-to-use alternative. Keep authoring notes and unused examples out of the finished project. Neither adopted form depends on this toolkit during ordinary work.

### Author a project workflow

The starter ships two workflows, [fix-bug](project-starter/workflows/fix-bug/SKILL.md) and [add-feature](project-starter/workflows/add-feature/SKILL.md). For another recurring task, use [templates/WORKFLOW.md](templates/WORKFLOW.md). It holds the authoring steps and one generic fenced block, not shipped examples, installed commands, or preselected recipes.

Write the block to `workflows/<chosen-name>/SKILL.md` in the project. Customize its skill sequence and task-specific modes or conditions, match its frontmatter `name` to the directory, and keep `disable-model-invocation: true`. Remove authoring instructions and outer fences. Keep procedures in the skills and policy in the project guide. The workflow's `../../agent-docs/DEVELOPMENT.md` pointer resolves from its final project directory; retain that guide even when no lifecycle is selected.

Users choose how to make generated workflows and their required skills available through their harness, following its current documentation. An unregistered workflow can be followed by filesystem path on the user's request where the host supports that entrypoint. If the host requires a native user command, use it rather than bypassing its manual-invocation gate. Preserve unrelated configured resources and never expose `templates/` or the toolkit's `project-starter/` as runnable skills. Changing live configuration requires separate explicit permission.

Copied guides and generated workflows are project-owned. Updating Null Stack does not overwrite them. Reading them does not authorize execution or publication, and individual skills remain usable on their own.

Check adopted or adapted guidance outside the toolkit checkout. Every retained local link and anchor must resolve from the consuming project, and required skills must be available for any integrations or workflows it adopts. Check the starter's public template link before distribution. Authoring instructions belong in the templates, not the finished project; the starter's empty factual sections and template pointer stay, as do formats for documents created during ordinary work.

## Skill packages

Each package keeps its entrypoint at `skills/<name>/SKILL.md`. Supporting documents live under `skills/<name>/resources/`; packages without support need no empty directory. Links between packages use relative filesystem paths, so shared support does not require a host-specific resource resolver.

For reusable guidance on descriptions, invocation choices, skill boundaries, and shared support, read [skill authoring](skills/agent-prose/resources/SKILL-AUTHORING.md). Use the target format and harness documentation for metadata and loading behavior.

## License

Null Stack's skills, workflows, templates, and documentation are licensed under the [MIT License](license).

You may use, modify, and redistribute the material, including commercially. Include the copyright and permission notices in copies or substantial portions. When copying material into another project, keep a copy of [license](license) alongside it or in the project's third-party license notices. You do not have to license the rest of your project under MIT.
