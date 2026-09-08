# Oh My Pi setup and reachability

Read this file when configuring Null Stack in Oh My Pi or checking whether OMP will discover, expose, or load an instruction file. These are host details, not requirements for running the skills in another agent tool. For runtime behavior not covered here, consult `omp://skills.md`, `omp://context-files.md`, or `omp://settings.md` in OMP.

## Use the public checkout

Keep one checkout of the public Null Stack repository. In the active OMP agent directory's `config.yml`, add the two library roots to `skills.customDirectories`. The default location is `~/.omp/agent/config.yml`; profiles and `PI_CODING_AGENT_DIR` can change the active agent directory.

```yaml
skills:
  enabled: true
  enableSkillCommands: true
  customDirectories:
    - "/absolute/path/to/null-stack/Skills"
    - "/absolute/path/to/null-stack/Workflows"
```

Replace the example paths with the checkout's absolute paths. Merge these entries into the existing configuration, retaining unrelated settings and skill roots. Array settings replace lower-precedence arrays rather than appending to them, so a project override must include every root that project still needs.

OMP scans one directory level below each custom root for `SKILL.md`. Register `Skills/` and `Workflows/`, not the repository root or `Templates/`. A custom-directory skill overrides a same-named provider skill; among custom directories, the first occurrence wins. Check duplicate names when switching checkouts so an older copy does not remain selected.

Check the configured roots with `omp config get skills.customDirectories --json`. Then start a new session and confirm that `/skill:intent` and `/skill:lifecycle` are available commands. To inspect the resolved files without running their procedures, ask that session to read `skill://intent` or `skill://lifecycle` as source material.

To run the shared lifecycle, the user explicitly invokes `/skill:lifecycle`. Its manual mode keeps it out of the model's offered skill list; it does not make the file unreadable.

## Adopt project guidance separately

Copy and customize the project starter independently of the shared library. Its `AGENTS.md` belongs at the consuming project root. The adjacent `agent-docs/` files are reached by task-specific pointers rather than inlined into every session.

`workflows/SKILL.md` in the starter is an optional example. Copying it does not register or adopt it. After customization, the user can explicitly ask the agent to follow that file without registering a command. To register it, choose a unique lowercase name, make the directory name match its frontmatter, and add that directory's parent to the project's skill roots. Preserve the central library roots when setting a project-level `skills.customDirectories` array. Keep `disable-model-invocation: true`.

Null Stack's root `AGENTS.md` is for maintaining this collection; it is not the project template or a user-level instruction file. Keep existing user instructions when setting up the library. Changing live agent configuration requires explicit authorization.

## Skill loading and resource paths

- A listed skill contributes its name and description to the model's available skills when the read tool is enabled. The body loads on demand through `skill://<name>`.
- `disable-model-invocation: true` normalizes to OMP's `hide` behavior. Hidden skills remain reachable through resource reads and, when `skills.enableSkillCommands` is enabled, `/skill:<name>`.
- A manual command injects the body with its base directory so relative paths can be resolved. Reading a workflow as source material is not permission to execute it.
- `skill://<name>` resolves to the skill's `SKILL.md`; `skill://<name>/<FILE>` resolves a resource inside that package. The resolver rejects absolute paths and `..` traversal. A workflow's project files must be read through filesystem paths, not a resource URI that tries to leave the package.
- `allowed-tools` has no documented enforcement behavior in OMP. It may describe expectations for other hosts, but the instructions cannot rely on it to grant or restrict tools.

## Context files and sticky rules

OMP loads context files at session start. One user context file survives provider precedence; native `~/.omp/agent/AGENTS.md` has the highest priority. Multiple project context files can survive at different directory depths, with farther ancestors injected first and the user context last.

Native project context comes from the nearest non-empty `.omp/` directory on the walk toward the repository root. If that directory lacks `AGENTS.md`, OMP does not continue to a farther `.omp/` directory for it. Standalone project `AGENTS.md` files use an ancestor walk; for repositories under the home directory, that walk can include enclosing workspace directories. Below-cwd context files are surfaced as paths to read before editing those directories rather than injected in full. Consult `omp://context-files.md` when exact location or precedence determines what loads.

In a context file, `@path` imports inline the target before injection. Use a relative Markdown link with an explicit read condition for optional guidance instead. A sentence saying to read an `@path` later does not defer its import.

`RULES.md` is sticky only at the native user agent directory and the selected native project `.omp/` directory. A user copy normally shadows a project copy rather than combining with it. Keep sticky rules short; they are not a substitute for conditional project guidance.
