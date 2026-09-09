# Oh My Pi setup and reachability

Read this file when configuring Null Stack in Oh My Pi or checking whether OMP will discover, expose, or load an instruction file. These are host details, not requirements for running the skills in another agent tool. For runtime behavior not covered here, consult `omp://skills.md`, `omp://context-files.md`, or `omp://settings.md` in OMP.

## Use the public checkout

Keep one checkout of the public Null Stack repository. With explicit permission to configure the host, add its `Skills/` root to `skills.customDirectories` in the active OMP agent directory's `config.yml`. The default location is `~/.omp/agent/config.yml`; profiles and `PI_CODING_AGENT_DIR` can change the active agent directory.

```yaml
skills:
  enabled: true
  enableSkillCommands: true
  customDirectories:
    - "/absolute/path/to/null-stack/Skills"
```

Replace the example path with the checkout's absolute path. Merge this entry into the existing configuration, retaining unrelated settings and skill roots. Array settings replace lower-precedence arrays rather than appending to them, so a project override must include every root that project still needs.

OMP scans one directory level below each custom root for `SKILL.md`. Register `Skills/`, not the repository root or `Templates/`. A custom-directory skill overrides a same-named provider skill; among custom directories, the first occurrence wins. Check duplicate names when switching checkouts so an older copy does not remain selected.

Check the configured roots with `omp config get skills.customDirectories --json`. Then start a new session and confirm that `/skill:intent` is available. To inspect its resolved file without running the procedure, ask that session to read `skill://intent` as source material.

The shared `Workflows/` root is retired. Existing users must separately authorize any live setup migration before replacing obsolete skill paths or removing that root. Preserve unrelated configured roots. Updating this checkout does not change live configuration or install resources.

## Adopt project guidance separately

Copy and customize the project starter independently of the shared library. Its `AGENTS.md` belongs at the consuming project root. The adjacent `agent-docs/` directory has five guides, reached by task-specific pointers rather than inlined into every session. The decision guide keeps record rules and format in the project without requiring an installed skill or resource resolver.

The starter's [agent-docs/development.md](../../Templates/Project/agent-docs/development.md) is the lifecycle policy's only template home. Follow its authoring instructions and replace the entire source with one adapted policy block or its explicit no-lifecycle option; do not retain outer fences or unused examples. It has no skill frontmatter or command. Skills own procedures and artifact semantics; the retained guide owns project policy choices and conditional pointers. A project can adopt policy without a task workflow. Individual skills remain available alone.

The starter contains no task workflows. To author one, use [Templates/Workflows/SKILL.md](../../Templates/Workflows/SKILL.md), a plain Markdown source document containing fenced full `SKILL.md` blocks for a generic template and labeled `fix-bug` and `add-feature` examples. It is not a registered or runnable skill, and those examples are not installed commands. Write the chosen block to `workflows/<chosen-name>/SKILL.md` in the project, removing authoring instructions, outer fences, and unused blocks. Keep only the skill sequence, task-specific modes or conditions, and project-guide pointer in the generated body.

Match the generated workflow's frontmatter `name` to its directory and keep `disable-model-invocation: true`. Copying guidance or generating a workflow does not adopt a lifecycle, register a command, or authorize execution. After customization and an explicit lifecycle choice, the user can ask the agent to follow `workflows/<chosen-name>/SKILL.md` by filesystem path without registering a command.

For optional command registration, add the consuming project's `workflows/` directory to its `skills.customDirectories` array. OMP scans the named workflow directories beneath that root. Never register `Templates/`. Preserve the central `Skills/` root and any unrelated roots the project needs because array overrides replace lower-precedence values:

```yaml
skills:
  enabled: true
  enableSkillCommands: true
  customDirectories:
    - "/absolute/path/to/null-stack/Skills"
    - "/absolute/path/to/project/workflows"
```

With separate permission to configure the host, replace the paths, merge the roots with existing settings, and check for duplicate names using the precedence rules above. Check `omp config get skills.customDirectories --json` from the consuming project, then start a new session. For example, if you generated a workflow named `review-change` in `workflows/review-change/`, confirm `/skill:review-change` is available and inspect `skill://review-change` as source without executing it. `review-change` is an example name, not a shipped command. The user invokes the generated workflow's command when they want to run it.

The generated workflow's `../../agent-docs/development.md` link must resolve from its final project directory through the filesystem, not through a `skill://` URI. Retain the project guide and keep OMP setup details here rather than in the generated workflow.

Keep existing user instructions when setting up the library. Changing live agent configuration requires explicit authorization.

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
