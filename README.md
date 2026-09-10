# Null Stack

A collection of agent skills, the copy-ready Project Starter, and authoring templates. Use a skill on its own, adopt the starter's defaults, or assemble project guidance and workflows to suit your work.

## What lives here

| Location | Purpose |
| --- | --- |
| [Skills/](Skills/) | Standalone capabilities, with supporting files inside each skill's directory |
| [Project Starter/](Project%20Starter/) | Opinionated, copy-ready project guidance with concrete defaults and empty sections for project-specific facts |
| [Templates/Project/AGENTS.md](Templates/Project/AGENTS.md) | Annotated project overview template, with its original instructions, examples, rules, and companion guides |
| [Templates/Project/agent-docs/code-style.md](Templates/Project/agent-docs/code-style.md) | Authoring template for code conventions, documentation, naming, and formatting |
| [Templates/Project/agent-docs/development.md](Templates/Project/agent-docs/development.md) | Authoring source for an optional project lifecycle policy |
| [Templates/Project/agent-docs/git.md](Templates/Project/agent-docs/git.md) | Authoring template for branching, commits, pull requests, and merges |
| [Templates/Project/agent-docs/linear.md](Templates/Project/agent-docs/linear.md) | Authoring template for Linear bindings and project-specific constraints |
| [Templates/Workflows/SKILL.md](Templates/Workflows/SKILL.md) | Plain Markdown authoring source with a generic workflow template and labeled `fix-bug` and `add-feature` examples |

A reusable skill owns its task procedure and artifact semantics, including revision and close-out. Project lifecycle policy chooses entry thresholds, artifact destinations, project approval gates and write rules, tracker event mapping, and effort completion. Short task workflows select skills and their order without repeating procedures or policy. Topic guides own Git conventions, Linear bindings and constraints, and lasting design decisions; shared skill defaults defer to project-owned record rules. Copying project guidance does not adopt a lifecycle or execute a workflow.

## Use the shared library

Keep one canonical checkout of `Skills/` rather than copying it into every project. Changes to that checkout affect the projects using it. To distribute an individual skill, follow [Share individual skills](#share-individual-skills).

Oh My Pi is the first supported host. For configuration, discovery precedence, manual invocation, and context loading, read [Oh My Pi setup and reachability](Skills/agent-prose/OH-MY-PI.md). This repository does not install resources or change an agent's live configuration automatically.

The instructions aim to be portable, but other hosts have not been verified. Skills can also need ordinary task tools such as Git, a runnable project, or the Linear CLI. A missing capability is not permission to install it.

Existing users must separately authorize any live setup migration. Replace obsolete central skill paths with the checkout's `Skills/` path and remove the retired shared `Workflows/` root, while preserving unrelated configured roots. `Templates/` is authoring source, never a discovery root.

## Share individual skills

Share the skill with all its required dependencies, including those reached through other packages.

1. Start with the skill's `SKILL.md` and follow its supporting-file pointers. Read every supported branch, including conditional ones, and identify instructions that require another skill or resource. Check references by name as well as links. A required read or handoff counts even if your first task will not trigger it; an optional adjacent suggestion, such as `test-quality`'s `shakedown` suggestion on request, does not.
2. Add the complete owning package for each required destination, then inspect that package's instructions and support in the same way. Repeat until every required destination belongs to an included package and no unread required references remain. Visit each package once so references back to an included package do not loop.
3. Copy those package directories with all their supporting files and a copy of [LICENSE](LICENSE). Preserve package names and internal paths. Keep shared rules in their owning package, as [Shared material](Skills/agent-prose/PACKAGING.md#shared-material) requires; do not paste a dependency's rules into the skill that uses them.
4. Make the copied packages discoverable through the destination host, then check every required read against the copied distribution with the original checkout and unrelated installed skills unavailable. Check both skill entry points and supporting-resource paths. For OMP, follow [setup and reachability](Skills/agent-prose/OH-MY-PI.md); other hosts need their own resolver. Reading support does not invoke its owning skill, and installing the packages does not adopt a workflow.

For example, [software-design/DEEPENING.md](Skills/software-design/DEEPENING.md) sends test-retirement decisions to the deletion gate in [test-quality/SKILL.md](Skills/test-quality/SKILL.md#deletion-gate). Include the complete `software-design/` and `test-quality/` packages, including `test-quality/ASSERTIONS.md` and `test-quality/DOUBLES.md`. Keep the gate in `test-quality`; this README and the copied `software-design` package should only point to it. This is one required dependency path, not the end of the discovery procedure: follow the remaining required references before declaring the distribution complete.

## Start a project

Copy the contents of [Project Starter/](Project%20Starter/) into the destination project without overwriting existing guidance. Include the entire `agent-docs/` directory, including `design-decisions/`. Preserve the toolkit's [license notice](#license) without replacing the destination project's license. For an existing project, reconcile its current instructions before adopting the starter.

```text
project/
  AGENTS.md
  agent-docs/
    git.md
    code-style.md
    linear.md
    development.md
    design-decisions/
      README.md
```

The starter's `AGENTS.md` keeps empty sections for the project name and purpose, tech stack, commands, and project structure. Fill them with confirmed facts when customizing; leaving them empty does not block ordinary work. The operating defaults, guide pointers, and permission rules are already filled in. The starter selects conservative Git conventions, follows the consuming repository's tooling, and keeps design-decision rules and format locally. It selects no formal development lifecycle or task workflows and configures no Linear integration.

For help filling project-specific sections, read the annotations and examples in the [AGENTS.md template](Templates/Project/AGENTS.md). The instructions live in the template itself, not in a separate customization guide. The starter's pointer names the source path and uses the public template URL so it survives copying. Ordinary work needs no network access, toolkit checkout, installed skills, or host-specific resolver.

To adopt a lifecycle, use [the lifecycle authoring template](Templates/Project/agent-docs/development.md) to write the project's `agent-docs/development.md`. Keep only the adapted policy block, without authoring instructions or outer fences. Adapt its links to the consuming overview, including the Rules anchor: the annotated template uses `#6-rules`, while the starter uses `#rules`. Policy and task workflows are separate choices; the starter's no-lifecycle default needs no further setup.

### Author a project AGENTS.md

Use [Templates/Project/AGENTS.md](Templates/Project/AGENTS.md) for the annotated template. It includes the original section instructions, filled examples, document pointers, rules, and "How to use this template" section. Copy it with its adjacent `agent-docs/` directory, then follow those instructions to adapt the overview and companion guides.

The template is authoring material; `Project Starter/` is the opinionated, ready-to-use alternative. Keep authoring notes and unused examples out of the finished project. Neither adopted form depends on this toolkit during ordinary work.

### Author a project workflow

The starter contains no workflow files. When a project needs one, use [Templates/Workflows/SKILL.md](Templates/Workflows/SKILL.md). It contains a generic template and labeled `fix-bug` and `add-feature` examples, not installed commands or preselected recipes.

Write the chosen block to `workflows/<chosen-name>/SKILL.md` in the project. Customize its skill sequence and task-specific modes or conditions, match its frontmatter `name` to the directory, and keep `disable-model-invocation: true`. Remove authoring instructions, outer fences, and unused blocks. Keep procedures in the skills and policy in the project guide. The workflow's `../../agent-docs/development.md` pointer resolves from its final project directory; retain that guide even when no lifecycle is selected.

The user can ask an agent to follow the generated workflow by filesystem path without registering a command. For optional host registration, follow [Oh My Pi setup and reachability](Skills/agent-prose/OH-MY-PI.md). Preserve unrelated configured roots and never register `Templates/` or the toolkit's `Project Starter/`. Changing live configuration requires separate explicit permission.

Copied guides and generated workflows are project-owned. Updating Null Stack does not overwrite them. Reading them does not authorize execution or publication, and individual skills remain usable on their own.

Check adopted or adapted guidance outside the toolkit checkout. Every retained local link and anchor must resolve from the consuming project, and required skills must be available for any integrations or workflows it adopts. Check the starter's public template link before distribution. Authoring instructions belong in the templates, not the finished project; the starter's empty factual sections and template pointer stay, as do formats for documents created during ordinary work.

## Packaging guidance

For resource layout, frontmatter, and supporting-file conventions, read [the packaging guidance](Skills/agent-prose/PACKAGING.md).

## License

Null Stack's skills, workflows, templates, and documentation are licensed under the [MIT License](LICENSE).

You may use, modify, and redistribute the material, including commercially. Include the copyright and permission notices in copies or substantial portions. When copying material into another project, keep a copy of [LICENSE](LICENSE) alongside it or in the project's third-party license notices. You do not have to license the rest of your project under MIT.
