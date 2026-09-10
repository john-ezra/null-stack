How Null Stack packages skills, workflows, and project templates. When configuring Oh My Pi or checking its discovery, invocation, resource URLs, or context-file behavior, read [OH-MY-PI.md](OH-MY-PI.md). Other hosts need their own loading rules; do not assume OMP behavior applies to them.

## Where a skill lives

A reusable skill is `skills/<name>/SKILL.md` with its supporting files in the same directory. A project-owned workflow composes skills and lives at `workflows/<name>/SKILL.md` in that project with the same frontmatter. A reusable skill owns its procedure and artifact semantics, including revision and close-out. Lifecycle policy chooses entry thresholds, destinations, project approval gates and write rules, tracker event mapping, and effort completion; short task workflows select skills and their order, plus task-specific modes or conditions.

Use lowercase kebab-case for directory and non-Markdown filenames, and uppercase hyphen-separated basenames with a lowercase `.md` extension for Markdown documents. Preserve tool-required filenames.


Keep a skill usable without adopting a workflow. A standalone invocation uses the user's requested destination or returns its result in the conversation; if persistence is required and no destination is known, resolve that before writing. Do not make a tracker or another workflow an implicit prerequisite.

The annotated project overview template lives at [templates/project/AGENTS.md](../../templates/project/AGENTS.md). Keep its instructions, examples, project rules, and "How to use this template" section in that file. Its adjacent `agent-docs/` directory contains the companion templates it references. Adapt the files together, following their authoring instructions, and remove editing notes and unused examples from the finished project. Do not replace the annotated overview with a blank skeleton or extract its instructions into a separate customization guide.

Project Starter provides opinionated, copy-ready guidance under `project-starter/` and becomes project-owned when adopted. Its `AGENTS.md` routes to five guides covering Git, code style, Linear, development, and design decisions. Operating defaults, guide pointers, and permission rules are filled in; project-specific factual sections remain empty. No formal lifecycle, Linear integration, or task workflows are selected.

The starter's customization-only pointer goes directly to the AGENTS.md template, using its public URL and naming `templates/project/AGENTS.md` as the source path. Toolkit documentation uses relative links to that file. Ordinary project work does not require the template, network access, the toolkit checkout, or a host-specific resolver. Keep skill-owned artifact formats in their packages and ongoing project document formats in their guides.

The [lifecycle authoring template](../../templates/project/agent-docs/DEVELOPMENT.md) contains bounded no-lifecycle and finite-effort blocks. Retain one adapted block in the consuming project's `agent-docs/DEVELOPMENT.md`, without authoring instructions, outer fences, or unused examples. Match its links to the consuming overview: the annotated template's Rules anchor is `#6-rules`; the starter's is `#rules`. A project can keep the starter's no-lifecycle guide, adopt policy without task workflows, or point to another chosen policy. Keep one policy authority and only a pointer in `AGENTS.md`.

The starter contains no task workflows. The separate [templates/workflows/SKILL.md](../../templates/workflows/SKILL.md) is a plain Markdown authoring document, not a registered or runnable skill. It contains fenced full `SKILL.md` blocks for a generic template and labeled `fix-bug` and `add-feature` examples. Generate only the chosen workflow at `workflows/<chosen-name>/SKILL.md` in the project, removing authoring instructions, outer fences, and unused blocks. Match its frontmatter name to its directory and keep `disable-model-invocation: true`.

Generated workflows contain only the skill sequence, task-specific modes or conditions, and a project-guide pointer. Their `../../agent-docs/DEVELOPMENT.md` link resolves from the final project workflow directory, not the authoring source. Keep procedures and artifact contents in the skills, lifecycle policy in the development guide, and setup mechanics in this packaging guidance and the host guide. Use relative filesystem links in generated project files, not host-specific resource URIs.

Copying the starter or authoring a workflow does not register a command or authorize execution. A project can keep the starter's no-lifecycle default when it authors a workflow. The user may request execution of a finished workflow by filesystem path without registration. If the host supports registration, add that project's `workflows/` alongside the central `skills/` root and preserve unrelated configured roots. Never register `templates/` or the toolkit's `project-starter/`; the shared `Workflows/` library root is retired. Read [OH-MY-PI.md](OH-MY-PI.md) for OMP configuration and commands. Existing users must separately authorize any live setup migration. Individual skills remain usable without a workflow or lifecycle.

## Frontmatter

Four fields are in use across the repo. Add no others.

- **`name`.** Matches the directory name for a registered package. Use a unique lowercase, hyphen-separated name. When naming or renaming a generated workflow, set both its directory and frontmatter to that name.
- **`description`.** One or two sentences, written by the rules below.
- **`disable-model-invocation`.** Present on every skill, directly after `description`, as an explicit `true` or `false`. It expresses manual or listed mode; it is not an access-control boundary. Workflows remain manual until the user explicitly changes that policy.
- **`allowed-tools`.** A `Bash(<cmd>:*)` list where needed by the host. Declare only the expected tools; do not treat metadata as authorization or assume the host enforces it.

## How a skill is reached

- **Listed skill.** Its description is the model-facing trigger. The body is loaded only when the task needs it.
- **Manual skill.** The user chooses when to invoke it. Other instructions may suggest it to the user, not dispatch it. Reading its source or supporting resources does not authorize execution.
- **Sibling files.** Use relative Markdown links from the body, such as `[GLOSSARY.md](GLOSSARY.md)`, with explicit read conditions. Refer to another skill's resource by its owning skill and resource path, using the current host's resolver where available.
- **Context files.** Keep the project overview and task-specific pointers in the project's context file. A pointer names the destination and the condition for reading it; an inline import cannot defer loading. Host-specific discovery, precedence, and sticky rules belong in the host guidance.

## Choosing listed or manual

Listed when the moment to use the skill is recognizable from an ordinary request without the user knowing the skill exists, or when other skills must route to it on their own. Manual when the moment is a human decision (`handoff` at the end of a session), when the user wants the choice kept in their hands, or when the skill would otherwise fire on requests it should not.

A description that claims permanent applicability ("always in force") makes the model read the body on every task; use that shape only for rules that apply to every turn.

## Writing the description

For a listed skill:

- **Name the job first.** The opening clause says what the skill does in the words a user's request would contain.
- **One trigger per path.** After the job, "Use when ..." lists the cases the body handles, one trigger each, synonyms collapsed into the trigger they share.
- **Promise exactly the body.** Every path the body handles on its own appears; nothing the body lacks is advertised.
- **No identity or explanation.** The body supplies both once opened; the description carries only what triggers.
- **"Not for" only against a real neighbour.** Add an exclusion when a neighbouring skill would otherwise catch the same request, in the neighbour's terms.

For a manual skill, one sentence naming the job; nothing matches on it, so a "Use when" clause is dead weight.

## When a skill earns separation

Split only when the halves have triggers users state differently, or when the later half must be hidden from the earlier one behind a real context boundary. File size and tidy organization are reasons for a sibling file behind a pointer, never for a skill. Merge test: two descriptions that would fire on the same requests are one skill.

## Shared material

Support that several skills use lives in one plain file with no frontmatter, inside the skill that owns the meaning. Link it relatively from there. From another skill, name the owning skill and resource behind a read condition. Reading support does not invoke its owning skill, regardless of either skill's listed or manual mode. Never create a third skill solely to hold shared text.

## Menu skill

A manual skill whose body is a list: each entry names a manual skill and gives the condition a person would recognize as the moment to run it. Use the host's explicit invocation form when one exists. The person invokes the entry; the body never tells the agent to.

## Bar

Every packaging decision on the skill has a verdict: its mode, each description rule, whether a split was earned, where each piece of shared material lives, whether any menu entry is written as if it could dispatch, and whether the frontmatter holds only the four fields above.
