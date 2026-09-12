# Code style

## Code conventions

Follow the affected code's established conventions and the rules enforced by the repository's tooling. Read nearby implementations before introducing a new pattern. When existing patterns conflict, prefer the maintained pattern used in the affected area; resolve a consequential ambiguity before changing it.

Keep style changes within the requested work. Do not add a formatter, linter, language dependency, or replacement convention merely to enforce a personal preference, and keep unrelated reformatting out of a change.

## Comments and documentation

A comment earns its place only by stating what the code cannot: a real constraint or a non-obvious why. Do not add design essays, per-field commentary, or justifications for choices recorded elsewhere.

Follow the repository's existing reference-documentation conventions for public interfaces. Update documentation when a change alters behavior it describes. Keep lasting design rationale in [design decisions](design-decisions/README.md); read that guide before creating or revising a record.

## Naming

Use the domain terms and naming patterns already present in the affected code and maintained documentation. Keep distinct concepts distinct; do not introduce synonyms for variety. Resolve conflicting domain meanings before spreading a new name across the codebase.

Name Markdown documents with uppercase hyphen-separated basenames and a lowercase `.md` extension, as in `CODE-STYLE.md`. Directories and other files follow the conventions of their language and tooling; where none apply, use lowercase kebab-case. Preserve tool-managed filenames.

## Markdown and prose

Use GitHub-flavored Markdown with ordinary links and image references, never wiki links or embeds that need a particular editor. Use relative paths for repository-local documents and assets. Do not manually wrap paragraphs; let the editor soft-wrap them. Never use em dashes; use a period or a comma instead.

Use `agent-prose` when writing or reviewing agent-facing instructions, including these guides and workflows. Use `natural-english` when writing or revising prose. Keep their procedures in those skills rather than repeating them here.

## Formatting

Use the repository's configured formatter and linter through its existing command definitions, as described in [repository evidence](../AGENTS.md#repository-evidence). If no formatter is configured, preserve the surrounding style.
