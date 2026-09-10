---
name: pr
description: Write pull request titles and bodies, or close out merged work. Use when opening or titling a PR, or recording delivery and closing its linked work after merge.
disable-model-invocation: false
---

Once merged, the PR's title and body are the permanent record of what changed and why. Write both so a reader who has never seen the conversation needs nothing else.

For post-merge close-out, use [After merge](#after-merge) instead of drafting a new PR.

## Ground

Nothing is drafted from memory of the work. Before the title:

1. **The change.** `git diff <base>...HEAD` and `git log --oneline <base>..HEAD`, where `<base>` is the branch the PR targets. Read the whole diff, not the last edit; the body describes everything the reviewer will see.
2. **The requirement.** The issue, spec, plan, or intent the work delivers against: issue keys and `Fixes #N` lines in the commits, a spec path the user named, or the plan the branch followed. Read it in full (`linear` for Linear mechanics). Its acceptance criteria become the Verification lines, and its route is what Decisions measures divergence from. With none, say so in Decisions rather than inventing one.
3. **The evidence.** The verification commands and their observed output, from this session or run now. A result nobody observed does not go in the body.

Done when the diff, the commit list, the requirement or its absence, and the observed verification output are all in hand.

## Title

Bare imperative. No type prefixes (`feat:`, `fix:`), no identifiers, no trailing period. It must pass the test:

> if you apply this PR it will …

"Add rate limiting to the login endpoint" passes. "Login fixes", "feat: rate limiting", and "Rate limiting" fail.

## Body

Use this template for every PR body, replacing the angle-bracket guidance:

```markdown
Issue: <the issue this work delivers against, as a plain identifier such as `WEB-12`; no closing keyword, so no tracker automation fires. Omit the line when there is no issue.>

## What & why

<2 to 4 sentences: what changed and why it was needed.>

## Decisions

<Anything a reviewer would question: the approach chosen over alternatives, tradeoffs accepted, divergence from the plan. Link design decision records where the project keeps them. "None" is a legitimate entry.>

## Verification

<What was actually run and what was observed: commands, output, the screenshot compared. Evidence, not assertion: "tests pass" fails this section; "`bun test auth`, 14 pass, 0 fail" passes. Where the work has a spec, one line per acceptance criterion: the check and what it showed.>
```

Done when: the grounding step has run, the title passes the apply-test with no prefix, the body follows the template above with every section filled and the issue line present whenever an issue exists, and Verification cites observed output, one line per acceptance criterion where a spec exists.

## After merge

1. Confirm the PR's repository, target branch, merged status, and merge commit on its host. Read any linked requirement, including approved amendments, or establish that none exists; read the shipped diff and verification evidence in either case. An open, approved, or closed-unmerged PR is not delivered work. Do not merge it as part of close-out. Done when actual merge evidence and the requirement or its confirmed absence are identified.
2. Prepare a close-out note identifying the PR and merge commit. If delivery diverged from the effective spec, say how; keep change-specific rationale in the PR and link lasting design records rather than copying them. Report any unmet criterion. Merge alone cannot turn unmet scope into completion; use `spec` when a scope decision is needed. Done when the note distinguishes shipped work from any unfinished obligation.
3. Resolve the requested destination and completion policy. A linked issue is not permission to write to its tracker. With permission, publish the note to that issue, then apply only the completion transition authorized by project policy or the request when its conditions are met. Use `linear` for Linear comments and explicit state updates. Without a tracker or write permission, return the note in chat; do not create records to close out a standalone PR. Effort completion and archival remain separate project decisions.
4. Confirm each authorized write at its destination. If the comment succeeds but the state update fails, report that partial result and the remaining transition; do not claim closure. Done when the user has the merge evidence, the close-out note or its published location, and the actual completion state.
