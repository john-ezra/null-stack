# Null Stack

A collection of agent skills and project templates. Use a skill on its own, adapt the starter for a project, or author a project-owned workflow.

## What lives here

| Location | Purpose |
| --- | --- |
| [Skills/](Skills/) | Standalone capabilities, with supporting files inside each skill's directory |
| [Templates/Project/](Templates/Project/) | Project guides, including an optional lifecycle policy, with no preselected task workflows |
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

Copy the contents of [Templates/Project/](Templates/Project/) into the destination project without overwriting existing guidance. Include the entire `agent-docs/` directory, including `design-decisions/`. Preserve the toolkit's [license notice](#license) without replacing the destination project's license. For an existing project, reconcile its current instructions before adopting the starter.

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

Fill the overview and the project-specific sections of the five guides using each file's authoring instructions. Replace examples with confirmed project facts and remove the editing notes when done. The overview routes to the guides and does not summarize lifecycle policy. The decision guide contains the project's record home, selection and maintenance rules, and record format; it needs no installed skill or harness-specific resource resolver and contains no sample accepted decisions.

The [development lifecycle template](Templates/Project/agent-docs/development.md) is an authoring document with bounded no-lifecycle and finite-effort blocks. Replace the entire file with one adapted block, without its outer fence, editing instructions, or unused examples. The finished guide holds project choices and conditional pointers, normally roughly 400-700 words; do not retain the authoring source or copy skill procedures into it. Confirm thresholds, artifact homes, approval and write rules, exact tracker mappings when used, resizing, and archive policy. You can adopt a lifecycle without task workflows, explicitly select no lifecycle, or point to another chosen policy. Keep one policy authority.

### Author a project workflow

The starter contains no workflow files. When a project needs one, use the separate [Templates/Workflows/SKILL.md](Templates/Workflows/SKILL.md) authoring source. It contains fenced full `SKILL.md` blocks: a generic template and labeled `fix-bug` and `add-feature` examples. Those examples are not installed commands or preselected project recipes. Do not register the authoring source.

```text
Templates/
  Workflows/
    SKILL.md          # Authoring source, not a generated workflow
```

Write the chosen block to `workflows/<chosen-name>/SKILL.md` in the project. Customize its skill sequence and task-specific modes or conditions, match its frontmatter `name` to the directory, and keep `disable-model-invocation: true`. Remove all authoring instructions, outer fences, and unused template or example blocks from the generated file. Keep skill procedures in the skills and lifecycle rules in the project guide. The workflow's `../../agent-docs/development.md` pointer resolves from its final project directory; retain that guide and make the project's policy choice explicit before running the workflow.

The user can ask an agent to follow `workflows/<chosen-name>/SKILL.md` by filesystem path without registering a command. For optional host registration, add that project's `workflows/` alongside the central `Skills/` root, preserving unrelated configured roots. Never register `Templates/`. Host-specific configuration and invocation belong in [Oh My Pi setup and reachability](Skills/agent-prose/OH-MY-PI.md). Changing live configuration requires separate explicit permission.

The copied guides and generated workflows are project-owned. Updating Null Stack does not overwrite them. Individual skills remain usable on their own.

Before using the completed starter, check it outside the toolkit checkout. Every retained local link and anchor must resolve from the consuming project, required skills must be available for adopted integrations or workflows, and the lifecycle choice must be explicit. No authoring instructions, outer example fences, unused examples, or host-specific resource URIs belong in the finished development guide. Reading the result does not authorize execution or publication.

## Packaging guidance

For resource layout, frontmatter, and supporting-file conventions, read [the packaging guidance](Skills/agent-prose/PACKAGING.md).

## License

Null Stack's skills, workflows, templates, and documentation are licensed under the [MIT License](LICENSE).

You may use, modify, and redistribute the material, including commercially. Include the copyright and permission notices in copies or substantial portions. When copying material into another project, keep a copy of [LICENSE](LICENSE) alongside it or in the project's third-party license notices. You do not have to license the rest of your project under MIT.
