How Null Stack packages skills, workflows, and project templates. When configuring Oh My Pi or checking its discovery, invocation, resource URLs, or context-file behavior, read [OH-MY-PI.md](OH-MY-PI.md). Other hosts need their own loading rules; do not assume OMP behavior applies to them.

## Where a skill lives

A reusable skill is `Skills/<name>/SKILL.md` with its supporting files in the same directory. A project-owned workflow composes skills and lives at `workflows/<name>/SKILL.md` in that project with the same frontmatter. A reusable skill owns its procedure and artifact semantics, including revision and close-out. Lifecycle policy chooses entry thresholds, destinations, project approval gates and write rules, tracker event mapping, and effort completion; short task workflows select skills and their order, plus task-specific modes or conditions.

Keep a skill usable without adopting a workflow. A standalone invocation uses the user's requested destination or returns its result in the conversation; if persistence is required and no destination is known, resolve that before writing. Do not make a tracker or another workflow an implicit prerequisite.

Project starter files live under `Templates/Project/` and become project-owned copies. Its `AGENTS.md` routes to the copied project guidance without adopting a lifecycle. The five guides cover Git, code style, Linear, development, and design decisions. The decision guide includes local record rules and format without requiring a skill package or host-specific resolver; shared skill defaults defer to those project-owned rules.

The starter's [agent-docs/development.md](../../Templates/Project/agent-docs/development.md) is the lifecycle policy's only template home. It is plain Markdown authoring material with no skill frontmatter, containing bounded no-lifecycle and finite-effort blocks. Replace the entire source with one adapted block, removing authoring instructions, outer fences, and unused examples. The retained guide contains project decisions and conditional owner pointers, normally roughly 400-700 words, not copied skill procedures. A project can explicitly adopt policy without task workflows, select no lifecycle, or point to another chosen policy. Keep one policy authority and only a pointer in `AGENTS.md`.

The starter contains no task workflows. The separate [Templates/Workflows/SKILL.md](../../Templates/Workflows/SKILL.md) is a plain Markdown authoring document, not a registered or runnable skill. It contains fenced full `SKILL.md` blocks for a generic template and labeled `fix-bug` and `add-feature` examples. Generate only the chosen workflow at `workflows/<chosen-name>/SKILL.md` in the project, removing authoring instructions, outer fences, and unused blocks. Match its frontmatter name to its directory and keep `disable-model-invocation: true`.

Generated workflows contain only the skill sequence, task-specific modes or conditions, and a project-guide pointer. Their `../../agent-docs/development.md` link resolves from the final project workflow directory, not the authoring source. Keep procedures and artifact contents in the skills, lifecycle policy in the development guide, and setup mechanics in this packaging guidance and the host guide. Use relative filesystem links in generated project files, not host-specific resource URIs.

Copying the starter or authoring a workflow does not adopt a lifecycle, register a command, or authorize execution. After customization and an explicit lifecycle choice, the user can ask an agent to follow a generated workflow by its filesystem path without registration. If the host supports registration, add that project's `workflows/` alongside the central `Skills/` root and preserve unrelated configured roots. Never register `Templates/`; the shared `Workflows/` library root is retired. Read [OH-MY-PI.md](OH-MY-PI.md) for OMP configuration and commands. Existing users must separately authorize any live setup migration. Individual skills remain usable without a workflow or lifecycle.

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
