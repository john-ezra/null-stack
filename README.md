# Null Stack

A collection of agent skills, the copy-ready Project Starter, and authoring templates. Use a skill on its own, adopt the starter's defaults, or assemble project guidance and workflows to suit your work.

## What lives here

| Location | Purpose |
| --- | --- |
| [skills/](skills/) | Standalone capabilities, with a root `SKILL.md` and supporting documents under each skill's `resources/` directory |
| [project-starter/](project-starter/) | Opinionated, copy-ready project guidance with concrete defaults and empty sections for project-specific facts |
| [templates/project/AGENTS.md](templates/project/AGENTS.md) | Annotated project overview template, with its original instructions, examples, rules, and companion guides |
| [templates/project/agent-docs/CODE-STYLE.md](templates/project/agent-docs/CODE-STYLE.md) | Authoring template for code conventions, documentation, naming, and formatting |
| [templates/project/agent-docs/DEVELOPMENT.md](templates/project/agent-docs/DEVELOPMENT.md) | Authoring source for an optional project lifecycle policy |
| [templates/project/agent-docs/GIT.md](templates/project/agent-docs/GIT.md) | Authoring template for branching, commits, pull requests, and merges |
| [templates/project/agent-docs/LINEAR.md](templates/project/agent-docs/LINEAR.md) | Authoring template for Linear bindings and project-specific constraints |
| [templates/workflows/SKILL.md](templates/workflows/SKILL.md) | Plain Markdown authoring source with a generic workflow template and labeled `fix-bug` and `add-feature` examples |

A reusable skill owns its task procedure and artifact semantics, including revision and close-out. Project lifecycle policy chooses entry thresholds, artifact destinations, project approval gates and write rules, tracker event mapping, and effort completion. Short task workflows select skills and their order without repeating procedures or policy. Topic guides own Git conventions, Linear bindings and constraints, and lasting design decisions; shared skill defaults defer to project-owned record rules. Copying project guidance does not adopt a lifecycle or execute a workflow.

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

Copy the contents of [project-starter/](project-starter/) into the destination project without overwriting existing guidance. Include the entire `agent-docs/` directory, including `design-decisions/`. Preserve the toolkit's [license notice](#license) without replacing the destination project's license. For an existing project, reconcile its current instructions before adopting the starter.

```text
project/
  AGENTS.md
  agent-docs/
    GIT.md
    CODE-STYLE.md
    LINEAR.md
    DEVELOPMENT.md
    design-decisions/
      README.md
```

The starter's `AGENTS.md` keeps empty sections for the project name and purpose, tech stack, commands, and project structure. Fill them with confirmed facts when customizing; leaving them empty does not block ordinary work. The operating defaults, guide pointers, and permission rules are already filled in. The starter selects conservative Git conventions, follows the consuming repository's tooling, and keeps design-decision rules and format locally. It selects no formal development lifecycle or task workflows and configures no Linear integration.

For help filling project-specific sections, read the annotations and examples in the [AGENTS.md template](templates/project/AGENTS.md). The instructions live in the template itself, not in a separate customization guide. The starter's pointer names the source path and uses the public template URL so it survives copying. Ordinary work needs no network access, toolkit checkout, installed skills, or host-specific resolver.

To adopt a lifecycle, use [the lifecycle authoring template](templates/project/agent-docs/DEVELOPMENT.md) to write the project's `agent-docs/DEVELOPMENT.md`. Keep only the adapted policy block, without authoring instructions or outer fences. Adapt its links to the consuming overview, including the Rules anchor: the annotated template uses `#6-rules`, while the starter uses `#rules`. Policy and task workflows are separate choices; the starter's no-lifecycle default needs no further setup.

### Author a project AGENTS.md

Use [templates/project/AGENTS.md](templates/project/AGENTS.md) for the annotated template. It includes the original section instructions, filled examples, document pointers, rules, and "How to use this template" section. Copy it with its adjacent `agent-docs/` directory, then follow those instructions to adapt the overview and companion guides.

The template is authoring material; `project-starter/` is the opinionated, ready-to-use alternative. Keep authoring notes and unused examples out of the finished project. Neither adopted form depends on this toolkit during ordinary work.

### Author a project workflow

The starter contains no workflow files. When a project needs one, use [templates/workflows/SKILL.md](templates/workflows/SKILL.md). It contains a generic template and labeled `fix-bug` and `add-feature` examples, not installed commands or preselected recipes.

Write the chosen block to `workflows/<chosen-name>/SKILL.md` in the project. Customize its skill sequence and task-specific modes or conditions, match its frontmatter `name` to the directory, and keep `disable-model-invocation: true`. Remove authoring instructions, outer fences, and unused blocks. Keep procedures in the skills and policy in the project guide. The workflow's `../../agent-docs/DEVELOPMENT.md` pointer resolves from its final project directory; retain that guide even when no lifecycle is selected.

Users choose how to make generated workflows and their required skills available through their harness, following its current documentation. An unregistered workflow can be followed by filesystem path on the user's request where the host supports that entrypoint. If the host requires a native user command, use it rather than bypassing its manual-invocation gate. Preserve unrelated configured resources and never expose `templates/` or the toolkit's `project-starter/` as runnable skills. Changing live configuration requires separate explicit permission.

Copied guides and generated workflows are project-owned. Updating Null Stack does not overwrite them. Reading them does not authorize execution or publication, and individual skills remain usable on their own.

Check adopted or adapted guidance outside the toolkit checkout. Every retained local link and anchor must resolve from the consuming project, and required skills must be available for any integrations or workflows it adopts. Check the starter's public template link before distribution. Authoring instructions belong in the templates, not the finished project; the starter's empty factual sections and template pointer stay, as do formats for documents created during ordinary work.

## Skill packages

Each package keeps its entrypoint at `skills/<name>/SKILL.md`. Supporting documents live under `skills/<name>/resources/`; packages without support need no empty directory. Links between packages use relative filesystem paths, so shared support does not require a host-specific resource resolver.

For reusable guidance on descriptions, invocation choices, skill boundaries, and shared support, read [skill authoring](skills/agent-prose/resources/SKILL-AUTHORING.md). Use the target format and harness documentation for metadata and loading behavior.

## License

Null Stack's skills, workflows, templates, and documentation are licensed under the [MIT License](license).

You may use, modify, and redistribute the material, including commercially. Include the copyright and permission notices in copies or substantial portions. When copying material into another project, keep a copy of [license](license) alongside it or in the project's third-party license notices. You do not have to license the rest of your project under MIT.
