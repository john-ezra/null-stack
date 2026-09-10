# Workflow template

This is authoring material, not a runnable workflow. Reading it does not invoke the template or either example.

## How to use

1. Choose a recurring task and read the skills it needs. Keep their procedures and artifact formats in those skills; the workflow names only their order and any task-specific modes or conditions.
2. Copy only the Template block or one filled example into the consuming project at `workflows/<name>/SKILL.md`. Replace the name, description, and steps. Use a unique lowercase, hyphen-separated name matching the directory, and keep `disable-model-invocation: true`.
3. Confirm the project's lifecycle guide before using the workflow. The blocks below assume `agent-docs/DEVELOPMENT.md`; their relative link resolves from the generated workflow, not from this source file. Adjust it to the project's actual guide. If the project needs lifecycle guidance, follow the [development lifecycle authoring source](../project/agent-docs/DEVELOPMENT.md) separately within the user's authorization. Write only the adapted policy to the consuming guide, never the authoring file. The guide may state that no lifecycle is selected; the workflow does not choose one.
4. Preserve each skill's invocation and approval rules. Keep artifact destinations and project permissions in the lifecycle guide, not in the recipe. A manual skill remains the user's to invoke, including at a session boundary.
5. Finish when the generated file contains only its frontmatter, policy pointer, and chosen sequence; no placeholders, editing instructions, or unselected examples remain; the named skills are available; and its retained links resolve inside the consuming project. Add an overview link only for a workflow the project actually keeps.
6. When the user requests execution, follow the finished workflow by file path within that request's scope. Authoring it is not an execution request. Command registration is optional and follows the consuming host's setup rules. Register generated workflow packages, never this authoring source or the toolkit's `templates/` directory.

## Template

```markdown
---
name: workflow-name
description: <One sentence naming the recurring task.>
disable-model-invocation: true
---

On explicit invocation, read the [development lifecycle](../../agent-docs/DEVELOPMENT.md), then use the named skills in order for the requested work.

1. `<skill-name>` with any task-specific mode or condition.
2. `<next-skill-name>`.
```

## Example: fix a bug

```markdown
---
name: fix-bug
description: Diagnose a bug, specify and challenge the repair, then implement it.
disable-model-invocation: true
---

On explicit invocation, read the [development lifecycle](../../agent-docs/DEVELOPMENT.md), then use the named skills in order for the requested work.

1. `diagnose` in diagnosis-only mode.
2. `spec` from the approved diagnosis report.
3. `plan` for the approved spec.
4. `shakedown` on the plan, if one was needed.
5. Implement and verify the approved fix.
```

## Example: add a feature

```markdown
---
name: add-feature
description: Shape, specify, plan, and implement a feature.
disable-model-invocation: true
---

On explicit invocation, read the [development lifecycle](../../agent-docs/DEVELOPMENT.md), then use the named skills in order for the requested work.

1. `shape` if the feature still needs decisions.
2. `intent` if the lifecycle calls for a finite effort.
3. `spec` from the approved intent or standalone requirement.
4. `plan` for the approved spec.
5. `shakedown` on the plan, if one was needed.
6. Implement and verify the approved feature slice.
```
