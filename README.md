# Null Stack

A collection of agent skills, shared workflows, and project templates. Use a skill on its own, invoke a shared workflow when you want its process, or adapt the starter for a project.

## What lives here

| Location | Purpose |
| --- | --- |
| [Skills/](Skills/) | Standalone capabilities, with supporting files inside each skill's directory |
| [Workflows/](Workflows/) | Shared processes that compose skills, assign artifact homes, and remain manually invoked |
| [Templates/Project/](Templates/Project/) | A workflow-neutral project starter, including an optional development-workflow example |
| [agent-docs/design-decisions/README.md](agent-docs/design-decisions/README.md) | Guide to this toolkit's public design-decision records |

A reusable skill owns what its artifact contains. A workflow owns where its work artifacts go and how they participate in the process. Project guides supply local facts and conventions, including the home for lasting design decisions; they do not silently adopt a workflow.

Before designing, changing, or reviewing an area of the toolkit, or creating or revising one of its design-decision records, read the [toolkit decision guide](agent-docs/design-decisions/README.md) and the relevant records it helps you find. These records concern Null Stack itself. The starter's decision directory is for a consuming project's own records; it does not copy the toolkit's decisions.

## Use the shared library

Keep one canonical checkout of `Skills/` and `Workflows/` rather than copying them into every project. Changes to that checkout affect the projects using it. Copy an individual skill with its supporting files and a copy of [LICENSE](LICENSE) when sharing it independently.

Oh My Pi is the first supported host. For configuration, discovery precedence, manual invocation, and context loading, read [Oh My Pi setup and reachability](Skills/agent-prose/OH-MY-PI.md). This repository does not install resources or change an agent's live configuration automatically.

The instructions aim to be portable, but other hosts have not been verified. Skills can also need ordinary task tools such as Git, a runnable project, or the Linear CLI. A missing capability is not permission to install it.

The shared [lifecycle](Workflows/lifecycle/SKILL.md) defines a Linear-based process. It is not a default imposed on every project. Invoke it explicitly when that is the process you want. Supply the consuming project's confirmed Linear context before using it; this library contains no configured workspace, team, or initiative.

## Start a project

Copy the contents of [Templates/Project/](Templates/Project/) into the destination project without overwriting existing guidance. Include the entire `agent-docs/` directory, including `design-decisions/`. Preserve the toolkit's [license notice](#license) without replacing the destination project's license. For an existing project, reconcile its current instructions before adopting the starter.

```text
project/
  AGENTS.md
  agent-docs/
    git.md
    code-style.md
    linear.md
    design-decisions/
      README.md
  workflows/
    SKILL.md
```

Fill the overview and the project-specific sections of the four guides using their editing instructions and labeled examples. Replace examples with confirmed project facts and remove the editing notes when done. The project overview routes to Git, code style, Linear, and design-decision guidance only when those topics are relevant. The decision guide locates the project's records and points to shared record guidance; it contains no sample accepted decisions. The overview contains no lifecycle or artifact-home table.

The [workflow example](Templates/Project/workflows/SKILL.md) is optional. It illustrates a development process using the existing skills and Linear, with artifact destinations and approval gates explained in the file. Review and adapt it before explicitly adopting it. If the project does not want the example, leave it out and remove its mention from the copied `AGENTS.md`. The other starter files and individual skills do not depend on it.

An adapted workflow is project-owned, like the copied guides. Updating Null Stack does not overwrite those copies. This differs from using a shared workflow directly from the canonical checkout.

Before using the completed starter, check that every retained local document link resolves inside the project, shared skill links resolve through the host, no example values remain as accidental configuration, and any workflow choice is explicit.

## Packaging guidance

For resource layout, frontmatter, and supporting-file conventions, read [the packaging guidance](Skills/agent-prose/PACKAGING.md).

## License

Null Stack's skills, workflows, templates, and documentation are licensed under the [MIT License](LICENSE).

You may use, modify, and redistribute the material, including commercially. Include the copyright and permission notices in copies or substantial portions. When copying material into another project, keep a copy of [LICENSE](LICENSE) alongside it or in the project's third-party license notices. You do not have to license the rest of your project under MIT.
