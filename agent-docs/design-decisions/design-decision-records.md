# Design decision records

Date: 2026-09-08

> Current best understanding, held for the recorded reasons. A better argument wins: update the record, don't route around it. Never silently obey a stale decision; never silently ignore a live one.

## Context

The toolkit separates artifact content from process. Skills own what an artifact contains, workflows choose where it participates in a process, and project guides supply local conventions. The [toolkit guide](../../README.md#what-lives-here) states that boundary. A consuming project can use the starter and individual skills without a workflow.

The [PR format](../../Skills/pr/SKILL.md#body) already links design decision records, and the [design skill](../../Skills/software-design/SKILL.md#strategic-not-tactical) reads relevant decisions before design work. Those references need a discoverable project home and shared rules for recording rationale that outlives a change.

## Decision

Keep lasting design rationale in repository files at `agent-docs/design-decisions/<slug>.md`, one decision per descriptive slug, without sequence numbers and with a date inside. Each project's `AGENTS.md` points to its decision guide for design, change, review, and record maintenance. The guide identifies the local home; [DECISIONS.md](../../Skills/software-design/DECISIONS.md) under `software-design` owns record content and maintenance.

Decisions can arise during shaping, planning, or implementation. Recording them is independent of any workflow or tracker. An accepted choice and permission to write its record are separate. Keep the records revisable when their reasoning changes, with dated explanations and preserved history.

## Reasons and alternatives

A PR records one change. A design decision gives later work one place to find the current choice, its reasons, and the conditions for changing it. Keeping lasting rationale only in plans or PRs would make readers reconstruct the current position from a series of past changes.

Putting the convention only in a workflow would leave projects that do not adopt that workflow without decision discovery. The project guide reaches the records without starting a process. Workflow references reuse that home instead of creating another one.

A support file under `software-design` keeps the format with the capability that reasons about design. A separate skill would add another entry to discover for the same task. Copying the format into each workflow would give the same rule multiple maintenance points.

## Consequences

Projects gain a guide and maintain records only for choices whose reasoning future work needs. Goals and work scope stay in intents or requirements, steps stay in plans, and change-specific rationale stays in PRs. Plans and PRs link lasting rationale.

The starter needs the shared decision-record support from the skill library, but it does not need a workflow or Linear. Copied guides are project-owned; they must keep their links usable outside the toolkit checkout.

Each record has one authoritative repository. Public rationale must stand on publicly accessible evidence, without private dependencies. Backfills must distinguish known reasons from unverified history.

## Reconsider when

Revisit this arrangement if projects repeatedly cannot discover the relevant records through their guides, if decision-record work develops a distinct process that warrants its own skill, or if the shared support cannot be reached in the supported standalone starter setup. Reconsider individual decisions when their recorded constraints or evidence change, rather than adding silent exceptions to them.
