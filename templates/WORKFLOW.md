# Workflow template

This is authoring material, not a runnable workflow. Reading it does not invoke the template.

## How to use

1. Choose a recurring task and read the skills it needs. Keep their procedures and artifact formats in those skills; the workflow names only their order and any task-specific modes or conditions.
2. Copy the Template block, without its outer fence, into the consuming project at `workflows/<name>/SKILL.md`. Replace the name, description, and steps. Use a unique lowercase, hyphen-separated name matching the directory, and keep `disable-model-invocation: true`. Project Starter ships two finished examples, `workflows/fix-bug/SKILL.md` and `workflows/add-feature/SKILL.md`.
3. Confirm the project's development policy before using the workflow. The block assumes `agent-docs/DEVELOPMENT.md`; its relative link resolves from the generated workflow, not from this file. Adjust it to the project's actual guide. If the project needs a policy, author it from `templates/DEVELOPMENT.md` separately, within the user's authorization. The guide may state that no lifecycle is selected; the workflow does not choose one.
4. Preserve each skill's invocation and approval rules. Keep artifact destinations and project permissions in the policy, not in the recipe. A manual skill remains the user's to invoke, including at a session boundary.
5. Finish when the generated file contains only its frontmatter, policy pointer, and chosen sequence; no placeholders or editing instructions remain; the named skills are available; and its retained links resolve inside the consuming project. Add an overview link only for a workflow the project actually keeps.
6. When the user requests execution, follow the finished workflow through an entrypoint the host supports. This may be a filesystem-path request or a native user command; keep the host's syntax outside the workflow. Authoring it is not an execution request. Users choose how to make generated workflow packages and their required skills available through their harness, following its current documentation. Keep required skill packages together in the library layout; never expose this file or the toolkit's `templates/` directory as runnable skills. Live setup requires separate permission.

## Template

```markdown
---
name: workflow-name
description: <One sentence naming the recurring task.>
disable-model-invocation: true
---

Run this workflow only when the user explicitly requests it. Reading its source or support does not authorize execution. On that request, read the [development policy](../../agent-docs/DEVELOPMENT.md), then use the named skills in order for the requested work.

1. `<skill-name>` with any task-specific mode or condition.
2. `<next-skill-name>`.
```
