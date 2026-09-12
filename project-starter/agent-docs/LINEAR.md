# Linear context

Read this guide before reading or writing Linear records for this project. It records the project's bindings and constraints. The `linear-cli` skill owns CLI mechanics, and the [development policy](DEVELOPMENT.md) owns artifact placement and lifecycle transitions.

## Two repositories

The Linear CLI reads its pin, `.linear.toml`, from the workspace root when one exists. Run Linear commands from the workspace root, and pass the workspace and team explicitly when a command must run from the project checkout. Do not copy the pin or this guide into the project repository.

## Project bindings

| Binding | Project value |
| --- | --- |
| Workspace | |
| Team | |
| Project selection | |
| Initiative association | |

An empty binding means it is not recorded here, not that any destination will do. Resolve the workspace and team from this table before accessing records; an authenticated account, CLI default, or similarly named project is not evidence of the right destination. When a needed binding is missing or ambiguous, ask the user before touching that destination. Keep credentials and tokens out of this file.

## Linear write permission

Read the current target before changing it. A request to start, pick up, or work on a named issue authorizes both pickup and completion updates. At pickup, confirm the target and its current state, then move it to `In Progress` before substantive investigation, planning, or implementation. Once its acceptance criteria are verified and any required merge or publication has succeeded, finish the [closeout steps](DEVELOPMENT.md#closeout), then move it to `Done` before reporting completion. A confirmed merge into the intended target branch counts; committing or pushing an unmerged branch does not. Confirm the resulting state after each update.

Use the team's exact existing state names. `In Progress` and `Done` are Linear's defaults; a team that renames them takes its own names.

Questions about an issue and requests only to inspect it are read-only. Every other write, including project-status changes, relations, and comments, requires authorization in the user's request. Approval of content is not permission to publish it or change tracker state. Follow [project write restrictions](../AGENTS.md#rules).

## Constraints

Preserve existing labels, priority, ownership, and state unless the request authorizes their change. Do not create labels or invent priorities to fit a request; resolve unavailable choices with the user. Leave new records unassigned unless the user names an owner, and do not infer an assignee from the authenticated account.

Confirm a destination's visibility before sending sensitive material, and keep credentials and private material out of destinations not authorized to receive them. Commit messages and PRs must make sense without tracker access; keep the association on the Linear side through the commit or PR URL.
