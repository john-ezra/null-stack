# *Project name*
---
*One or two sentences: what the project is and does.*

```
Example: A Go orchestrator that dispatches coding-agent workers to tmux on a remote host over SSH.
```

## 1. Tech stack
---
*Names only, no versions; the manifests own those. Prioritize what an agent would otherwise guess wrong: the package manager, the odd choice, the nonstandard invocation.*

```
Example:

- Next.js
- Tanstack Router
- Supabase
- Vercel
```

## 2. Commands
---
*Point to the single home where commands live and how to enumerate them (package.json scripts, a justfile, a Makefile). Inline only what the home can't express: the single-test form, a required env var, a service that must be running.*

```
Example: Commands are package.json scripts, run with bun (`bun run <script>`). One-off test: `bun test path/to/file.test.ts`.
```

## 3. Project structure
---
*Top-level directories only, one line each: what lives where. Deeper structure is discoverable; prose copies of it drift.*

```
Example:

- cmd/: entrypoints
- internal/orchestrator/: dispatch core
- internal/transport/: SSH and tmux plumbing
- agent-docs/: project guidance; mapped in Agent docs below
```

## 4. Development process
---
*Point to agent-docs/development.md for the project's lifecycle choice; do not summarize its policy here. Replace that authoring template with a compact policy or its explicit no-lifecycle option. Task workflows are authored separately; list and link only those actually created for this project, or state that none are selected.*

```
Example:

Read the [development lifecycle](agent-docs/development.md) for our policy choice, artifact homes, and approval rules. No task workflows have been selected.
```

Project guidance and individual skills remain usable without adopting a workflow. Read or run a task workflow only on explicit request.

## 5. Agent docs
---
One home per kind of information; a fact lives in its home, everywhere else points to it. A change that invalidates a doc updates that doc in the same change.

| Read | When |
| --- | --- |
| [Development lifecycle](agent-docs/development.md) | Before scoping, planning, implementing, reviewing, publishing, or closing out project work |
| [Git conventions](agent-docs/git.md) | Before any Git operation or PR work |
| [Code style](agent-docs/code-style.md) | Before the first code or documentation edit in a session |
| [Linear context](agent-docs/linear.md) | Before reading or writing Linear records for this project |
| [Design decisions](agent-docs/design-decisions/README.md) | Before designing, changing, or reviewing an area, or creating or revising a design-decision record |

## 6. Rules
---
A rule lives here only if no event can trigger reading it, or violating it is hard to reverse; everything else belongs in a file above.

- Git: commit, push, or amend only when explicitly asked; never work directly on main; feature-branch first; `git add` exact paths only, never `-A` or `-a`.
- Linear: create, update, move, or comment on records only when explicitly asked. Approval of content is not permission to publish it or change tracker state.

*Add the project's ambient prohibitions: rules with no trigger moment that must hold on every line of output: vocabulary bans, cleanroom constraints, forbidden targets.*

```
Example: No nautical language: naming, docs, comments, and identifiers never use nautical or maritime vocabulary. This is cleanroom development alongside a related project; shared vocabulary must not creep in.
```

## 7. Working with the operator
---
*Project-specific collaboration rules only: the mode of working that is a fact about this project (teaching stance, decision process, review cadence). Delete the section if this project has nothing special to say.*

```
Example: Teach while building. When a Go idiom or a design move shows up in the work, explain in a sentence or two why it is shaped that way.
```

## How to use this template
---
1. Copy this file as the project's `AGENTS.md` and the entire `agent-docs/` directory beside it, including `development.md` and `design-decisions/README.md`. Fill the project-specific sections of the guides as well as this overview.
2. In this overview, unlabeled text, bullets, and the table are project content. Retain them unless the project differs. Each guide supplies its own authoring instructions.
3. Italic text is an editing instruction. Replace it with project facts, or remove the section when it does not apply.
4. Fenced blocks labeled "Example:" illustrate filled content, not project facts. Delete them after filling each section.
5. Replace the entire `agent-docs/development.md` authoring source with one adapted policy block or an explicit no-lifecycle choice, without its outer fence, authoring instructions, or unused examples. Keep lifecycle policy there and only its pointer here. Author task workflows separately using the toolkit's workflow template, and add overview links only after their files exist. Copying the starter adopts neither a lifecycle nor a workflow, and reading the guide authorizes no execution or publication.
6. Remove this section when the starter is filled. Completion means the project's choices are explicit, no editing instructions or unused examples remain, and every retained document link and anchor resolves from the consuming project.
