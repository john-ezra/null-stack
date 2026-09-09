# Code style
---
- A comment earns its place only by stating what the code cannot: a real constraint or a non-obvious why.
- Never: design essays, per-field commentary, or justifying choices recorded elsewhere.

*Fill the sections below with language-bound conventions for this repo. Name exceptions to existing tooling or language norms, rather than restating both. Delete the editing instructions and examples when filled. Replace these sections if the stack changes.*

## Code conventions

*Record language-specific code rules that naming and formatting do not cover.*

```
Example: In TypeScript, do not introduce `any`. Use a concrete type, or use `unknown` and narrow it before accessing its value.
```

## Documentation

*Name the reference documentation and which declarations need it. Cover godoc, JSDoc, or docstrings as applicable.*

```
Example: Godoc is the reference documentation: every package opens with a package comment saying what it is for; exported identifiers carry godoc starting with the name.
```

## Naming

*Record project-specific naming rules and terms an agent could otherwise get wrong.*

```
Example: Use customer for the billing account and user for an individual login. Keep those names distinct in identifiers and docs.
```

## Formatting

*Name the formatter and its configuration home. Point to the command home recorded in AGENTS.md rather than copying command recipes.*

```
Example: Prettier owns formatting; configuration lives in package.json. Use the formatting script from the command home in AGENTS.md.
```
