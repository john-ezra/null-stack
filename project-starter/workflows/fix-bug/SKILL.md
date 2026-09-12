---
name: fix-bug
description: Diagnose a bug, specify and challenge the repair, then implement it.
disable-model-invocation: true
---

Run this workflow only when the user explicitly requests it. Reading its source or support does not authorize execution. On that request, read the [development policy](../../agent-docs/DEVELOPMENT.md), then use the named skills in order for the requested work.

1. `diagnose` in diagnosis-only mode.
2. `spec` from the approved diagnosis report.
3. `plan` for the approved spec.
4. `shakedown` on the plan, if one was needed.
5. Implement and verify the approved fix.
