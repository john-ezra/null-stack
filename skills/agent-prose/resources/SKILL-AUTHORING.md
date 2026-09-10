# Skill authoring

Use this resource when deciding a skill's metadata, invocation policy, description, separation, or shared support. Follow the target skill format and actual project conventions. When a decision depends on discovery, loading, metadata semantics, or invocation mechanisms, consult the target harness's current documentation rather than borrowing another host's behavior.

## Ownership and standalone use

A reusable skill owns its procedure and artifact semantics, including revision and close-out. A workflow chooses skills and their order, plus task-specific modes or conditions. Keep project approval gates, destinations, write rules, and tracker policy in project guidance rather than making them part of a reusable procedure.

Keep a skill usable without adopting a workflow. A standalone invocation uses the user's requested destination or returns its result in the conversation; if persistence is required and no destination is known, resolve that before writing. Do not make a tracker or another workflow an implicit prerequisite.

## Metadata

Use the fields supported by the target format and harness, following the project's conventions for names and layout. Check required fields, accepted values, and their documented effects before adding or changing them. A field supported by one host need not exist or mean the same thing on another.

State the intended invocation policy separately from how the host implements it. Metadata may affect discovery, automatic selection, explicit invocation, or tool availability differently. Treat a visibility or invocation setting as access control only when the host documents an enforcement guarantee. Tool metadata describes or constrains capability; it does not grant permission to act.

## How a skill is reached

- **Listed skill.** Make its description a model-facing trigger wherever the host exposes it for automatic selection. Check how the body loads rather than assuming selection and loading are the same operation.
- **Manual skill.** The user chooses when to invoke it. Other instructions may suggest it to the user, not dispatch it. Reading its source or supporting resources does not authorize execution.
- **Supporting files.** Use relative Markdown links with explicit read conditions. For shared support in another package, identify the owning skill and link to the resource by its relative filesystem path. Check resolution from the file that contains the link.
- **Context files.** Keep the project overview and task-specific pointers in the project's context file. Use a conditional pointer for material that only some tasks need. If the host eagerly expands an import, wording that asks for a later read cannot defer that expansion; consult its documentation when import behavior affects placement.

## Choosing listed or manual

Listed when the moment to use the skill is recognizable from an ordinary request without the user knowing the skill exists, or when other skills must route to it on their own. Manual when the moment is a human decision (`handoff` at the end of a session), when the user wants the choice kept in their hands, or when the skill would otherwise fire on requests it should not.

A description that claims permanent applicability ("always in force") asks the model to select the skill on every task where that description is visible. Use that shape only for rules that apply to every such task.

## Writing the description

For a listed skill:

- **Name the job first.** The opening clause says what the skill does in the words a user's request would contain.
- **One trigger per path.** After the job, "Use when ..." lists the cases the body handles, one trigger each, synonyms collapsed into the trigger they share.
- **Promise exactly the body.** Every path the body handles on its own appears; nothing the body lacks is advertised.
- **No identity or explanation.** The body supplies both once opened; the description carries only what triggers.
- **"Not for" only against a real neighbour.** Add an exclusion when a neighbouring skill would otherwise catch the same request, in the neighbour's terms.

For a manual skill, name the job in one sentence. Add a human-facing invocation condition when the host's description display needs it; do not write it as permission for automatic dispatch.

## When a skill earns separation

Split only when the halves have triggers users state differently, or when the later half must be hidden from the earlier one behind a real context boundary. File size and tidy organization are reasons for a sibling file behind a pointer, never for a skill. Merge test: two descriptions that would fire on the same requests are one skill.

## Shared material

Support that several skills use lives in one plain file, inside the skill that owns the meaning. Keep it a resource rather than a separately registered skill. Link to it with a relative Markdown path and a read condition, naming the owning skill when linking from another package. Reading support does not invoke its owning skill, regardless of either skill's listed or manual policy. Never create a third skill solely to hold shared text.

## Menu skill

A manual skill whose body is a list: each entry names a manual skill and gives the condition a person would recognize as the moment to run it. Use the host's documented explicit invocation form when one exists. The person invokes the entry; the body never tells the agent to.

## Bar

Every authoring decision on the skill has a verdict: its intended invocation policy, each description rule, whether a split was earned, where each piece of shared material lives, whether any menu entry is written as if it could dispatch, and whether its metadata and resource paths fit the target format, harness, and project conventions. Any claim about host discovery, loading, or enforcement has support in that host's documentation.
