---
name: conformance
description: Audit a change set against the requirements that originated it. Not a code review; never run unasked.
disable-model-invocation: true
---

Read-only audit of whether a change set does what its originating requirements asked, no more and no less. Non-goals, which belong to the repository's ordinary review: code quality, style, security, test adequacy, and general defects. Fix nothing, propose no fixes, and never reconstruct requirements the authoritative sources do not state.

## 1. Pin the comparison

1. **Get a reference.** The user supplies a commit, branch, tag, or any revision expression. With none, ask and do not start; never fall back to `HEAD`'s parent or a guessed base branch.
2. **Capture the commits.** Record the repository root (`git rev-parse --show-toplevel`) and the current branch name, if any, for provenance lookup. Resolve the supplied reference with `git rev-parse --verify --end-of-options '<ref>^{commit}'` and `HEAD` with `git rev-parse --verify 'HEAD^{commit}'`. Save their full object IDs as `<base-oid>` and `<target-oid>`. Resolve and save `<merge-base-oid>` with `git merge-base <base-oid> <target-oid>`. If either revision fails to resolve or there is no merge base, report the blocker and stop before comparing.
3. **Pin the diff.** Record `git diff <merge-base-oid> <target-oid>` with the captured IDs substituted. This preserves the three-dot comparison's merge-base-to-target semantics; it is not a diff from the supplied base's tip. Every later comparison uses these endpoints, narrowed with `-- <path>` when needed. Run all commands in the recorded repository. Never resolve the input reference or `HEAD` again during this audit, even if either moves. If `git status --porcelain` is nonempty and the user asked about their working state, say the audit stops at the captured target commit and let them commit first.
4. **Get the commit list.** Record `git log --oneline <base-oid>..<target-oid>` beside the diff command. This is the directed list of commits reachable from the target but not the supplied base, not a merge-base-to-target list. Use these same IDs when reading full commit messages.
5. **Check for changes.** Run `git diff --stat <merge-base-oid> <target-oid>`; if it prints nothing, report an empty comparison with the captured IDs and stop.

Use Git object reads for all implementation evidence, including unchanged files. List paths with `git ls-tree -r --name-only <target-oid>`, read a file with `git show <target-oid>:<path>`, and search with `git grep -n -e '<pattern>' <target-oid> -- <paths>`. Omit the path restriction when the search needs the whole tree. Parent and scout use the same captured target, never the current checkout, index, or untracked implementation. These reads require no checkout, reset, stash, or worktree creation. If an object cannot be read, report the blocker rather than substitute the current working tree.

Done when the full base, target, and merge-base IDs and both commands are recorded, and the pinned diff is nonempty.

## 2. Establish the authoritative source set

The sources are the contracts that originated the work. Commit messages and the PR body can establish provenance by pointing at them, but are never requirement sources themselves. Search these locations in order, following explicit provenance links and resolving all candidates that may govern the change. Finding one source does not exclude another:

1. **Linked work items.** Collect every reference on the change: issue keys (`WEB-12`), `Linear-issue:` trailers, and `Fixes #N` or `Closes #N` lines across the whole pinned commit list, `linear issue id` for the recorded branch, and `gh pr view` for issues linked from its PR. Use the recorded branch explicitly for these lookups, not a later checkout's branch; for a detached target, use an established PR or work-item identifier. Retrieve each in full with `linear issue view <ID> --json` (read `linear-cli` for mechanics first) or `gh issue view <N> --comments`; a comment that amends the requirement governs. Establish which items the commits deliver against and which are only related references. Collecting a reference does not make it authoritative. A Linear issue's description is its requirement contract; the Plan document attached to it is the route, not a source.
2. **A PRD or local spec path the user supplied.** Include it when the user says it originated the work or an explicit provenance link establishes that role.
3. **The working tree.** Search for files whose names or headings share words with the recorded branch or feature, in order: `agent-docs/` (intents and archive), then `docs/`, `specs/`, `spec/`, `design/`, `rfcs/`, then root-level markdown. Use `glob` with gitignore off so untracked planning files count. These matches are candidates only. Require an explicit provenance link or user confirmation before treating one as an originating contract. This working-tree search discovers requirement sources only; it does not supply implementation evidence.
4. **The user.** Ask them to resolve any remaining uncertainty about which sources govern. If they cannot establish an authoritative source set, report that blocker and stop; never reconstruct requirements from the code, the tests, the PR description, or what the feature appears to be for.

Record each included source's identifier and provenance, read it in full with amendments, and map every operative requirement to its source citation. Follow requirement-source links by their meaning, not by a particular field name. When sources conflict and no amendment or explicit precedence settles them, ask the user before continuing.

Done when the authoritative source set is established, every source has been read in full, and every operative requirement maps to its source.

## 3. Brief one scout

Dispatch exactly one read-only `scout` through `task`, as a single-item batch. Give it the recorded repository path and all three full commit IDs, the commands with those IDs substituted, and every authoritative source by path or as the complete retrieved text, never a summary. Include the provenance record and requirement-to-source map.

```markdown
# Target
Repository: <recorded repository root; run every Git command here>
Base: <base-oid>; target: <target-oid>; merge base: <merge-base-oid>
Pinned diff: `git diff <merge-base-oid> <target-oid>` (merge-base-to-target; narrow with `-- <path>`)
Commits: `git log --oneline <base-oid>..<target-oid>` (target commits not reachable from the base)
Implementation reads: `git ls-tree -r --name-only <target-oid>`, `git show <target-oid>:<path>`, and `git grep -n -e '<pattern>' <target-oid> -- <paths>`; omit `<paths>` and `--` for a whole-tree search. Do not use the checkout as implementation evidence or resolve moving references.
Sources: <each authoritative source's identifier, provenance, and path or full text, with the requirement-to-source map>

# Change
Compare the authoritative requirements to the pinned diff and the resulting implementation at the captured target commit. Read unchanged implementation from that same target as needed to establish whether requirements are already met; do not expand the audit into unrelated existing behavior. Report candidates in three classes only:
1. Omitted or partial: a stated requirement the resulting implementation does not meet, or meets incompletely.
2. Unrequested: behavior the diff adds that no requirement in the authoritative source set asked for, however well built.
3. Incorrect: a requirement the diff implements in a way that contradicts what it states.
Do not report code quality, style, naming, tests, security, performance, design, or bugs unrelated to a stated requirement.

# Acceptance
Each candidate carries its class, the requirement quoted in full with its source identifier and location, and one sentence stating the disagreement. For implemented behavior, include the file and hunk (`@@` header or line range) in the pinned diff. For an omission with no hunk, provide absence evidence instead: the relevant or expected implementation location, the target commit ID, the search scope and queries, and the results showing the requirement is not met. Search the pinned diff and relevant implementation at the captured target, including unchanged code, before claiming an omission. Drop candidates missing the citation or the evidence appropriate to their class. Return candidates, not conclusions.
```

Done when the candidate list is back; nothing in it is a finding yet.

## 4. Verify every candidate yourself

A candidate is confirmed against its authoritative requirement and implementation evidence or it is gone:

- **The citation.** Reread it in context in the identified source and confirm it is an operative requirement, not background, an example, a rejected alternative, an open question, or work marked deferred or out of scope. Check other authoritative sources and amendments for qualifications.
- **The hunk or absence evidence.** For a cited hunk, run `git diff <merge-base-oid> <target-oid> -- <file>` and confirm it says what the scout said it says. An omission needs no hunk. Instead, check the full requirement citation, the relevant or expected implementation location at the captured target, and the recorded search scope, queries, and results.
- **Omitted or partial.** Search the whole pinned diff and relevant implementation at the captured target before accepting the omission; another file, helper, config entry, migration, test fixture, or unchanged implementation may already carry the behavior. `git diff --stat <merge-base-oid> <target-oid>` lists touched files, not every possible implementation location. Repeat the searches against target objects and record their results.
- **Unrequested.** Check the entire authoritative requirement set before declaring behavior unrequested. Confirm the behavior is new, not pre-existing code moved, renamed, or reformatted: `git diff -M -w <merge-base-oid> <target-oid> -- <file>`, and for a block that still looks added, `git grep -n -F -e '<a distinctive line>' <merge-base-oid>`.
- **Incorrect.** The contradiction is between the diff and the requirement's text, not between the diff and how you would have built it; a preference is a review comment, not a finding.
- **Drop what does not confirm.** No "possible", "worth checking", or "the scout suggested" reaches the report, and dropped candidates are never mentioned.

A conforming verdict is also a claim: walk every authoritative source's acceptance criteria once yourself against the pinned diff and resulting implementation at the captured target, including relevant unchanged code read from that commit. The scout's silence on one is not evidence.

Done when every candidate is confirmed or discarded and every acceptance criterion in the source set has been checked once with its source recorded.

## 5. Report

Order findings by impact; at comparable impact, omitted or incorrect outranks unrequested.

```markdown
Verdict: <one line: N findings against <source identifiers>, or conforms>
Sources: <each authoritative source's identifier, location, amendments, and provenance>
Repository: <recorded repository root>
Base: <full base-oid>; target: <full target-oid>; merge base: <full merge-base-oid>
Comparison: `git diff <merge-base-oid> <target-oid>` (merge-base-to-target, preserving three-dot semantics)
Commits: `git log --oneline <base-oid>..<target-oid>` (target commits not reachable from the base)

## Findings

1. <Omitted | Partial | Unrequested | Incorrect>. <one line naming the disagreement>
   Requirement: "<the requirement quoted in full, enough to keep its meaning>" (<source identifier, section or comment; include other governing citations when needed>)
   Change: <what the diff does, or what the resulting implementation fails to do, one or two sentences>
   Evidence: <for implemented behavior: file and pinned-diff hunk header or line range; for an omission without a hunk: relevant or expected implementation location, search scope and queries, and results covering the pinned diff and implementation at the captured target, including unchanged code>

Summary: <N> confirmed findings; highest impact is #1, <one clause>.
```

A citation shortened until it loses a condition is a misquote. With no confirmed findings, replace the findings section with one sentence: the change set conforms to the authoritative source set as written, listing its identifiers. An unresolved reference, an empty diff, or an unestablished source set is reported as only that blocking result, with no verdict.

Done when every template field is filled and each finding maps to its governing sources, or the conforming sentence stands in place of the findings.

## Routing

`shape` for an unclear problem statement; `intent` for capturing a wanted outcome; `spec` for turning an authoritative requirement into a spec; `plan` for implementation breakdown; `software-design` for architecture and test-seam questions; `shakedown` for adversarial pressure on a proposal; `pr` for pull-request preparation; `handoff` for transition material; `natural-english` for the report's prose, never its scope; `linear-cli` for Linear command mechanics.
