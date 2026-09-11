# Project guidance

When customizing this file, read the [AGENTS.md template](https://github.com/john-ezra/null-stack/blob/main/templates/project/AGENTS.md), source `templates/project/AGENTS.md` in the Null Stack checkout. Its annotations and examples explain what belongs in each section. Unfilled sections mean the information is not recorded here, not that setup must finish before work can begin. Use repository evidence when the task needs those facts.

## Project name and purpose

## Tech stack

## Commands

## Project structure

## Repository evidence

Read the repository's maintained documentation, manifests, configuration, and affected source before choosing tools or changing code. Use them to identify the stack, package manager, architecture, and commands. Do not assume a language, runtime, service, or command from these guides.

Use the existing command definitions and CI configuration for build, test, lint, and formatting commands. If the repository provides no command for a needed check, choose a check supported by its actual tools and explain any verification gap.

## Agent docs

One home per kind of information; a fact lives in its home, everywhere else points to it. A change that invalidates a doc updates that doc in the same change.

| Read | When |
| --- | --- |
| [Project outline](agent-docs/PROJECT-OUTLINE.md) | When understanding the project or considering changes to its purpose, capabilities, or scope |
| [Research](agent-docs/research/README.md) | Before investigating a topic or making a decision that prior research may inform |
| [Development policy](agent-docs/DEVELOPMENT.md) | Before scoping, planning, implementing, reviewing, publishing, or closing out project work |
| [Git conventions](agent-docs/GIT.md) | Before any Git operation or PR work |
| [Code style](agent-docs/CODE-STYLE.md) | Before the first code or documentation edit in a session |
| [Linear context](agent-docs/LINEAR.md) | Before reading or writing Linear records for this project |
| [Design decisions](agent-docs/design-decisions/README.md) | Before designing, changing, or reviewing an area, or creating or revising a design-decision record |

## Rules

- Change files only within the user's authorized scope. Approval of a proposal's content alone is not permission to edit files, execute it, or publish it.
- Commit, push, amend, open or update a PR, or merge only when explicitly asked. Never work directly on the repository's default branch; use a feature or fix branch first. Stage exact paths only, never all changes with `git add -A`, `git add .`, or `git commit -a`.
- Preserve unrelated work and private files. Deletion or history rewriting requires explicit permission.
- Create, update, move, or comment on Linear records only when explicitly asked. Approval of content is not permission to publish it or change tracker state.
- Repository edits do not authorize installation, live configuration changes, releases, or deployment. Resolve missing permission before taking those actions.
