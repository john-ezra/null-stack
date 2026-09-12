---
name: add-feature
description: Shape, specify, plan, and implement a feature.
disable-model-invocation: true
---

Run this workflow only when the user explicitly requests it. Reading its source or support does not authorize execution. On that request, read the [development policy](../../agent-docs/DEVELOPMENT.md), then use the named skills in order for the requested work.

1. `shape` if the feature still needs decisions.
2. `intent` if the policy calls for a finite effort.
3. `spec` from the approved intent or standalone requirement.
4. `plan` for the approved spec.
5. `shakedown` on the plan, if one was needed.
6. Implement and verify the approved feature slice.
