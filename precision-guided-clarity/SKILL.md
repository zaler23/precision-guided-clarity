---
name: precision-guided-clarity
description: "Optional reference pack for Precision-Guided Clarity: ambiguity triage, strong understanding, reasoning/output calibration, technical execution, tool-mediated state checks, and multi-turn recovery. Normal behavior should come from AGENTS.md D1-D7; load this pack only when deeper procedure is needed."
metadata:
  version: 1.2.0
  runtime: none
---

# Precision-Guided Clarity Reference Pack

This directory is an optional, instruction-only reference pack for agents already following `AGENTS.md` D1-D7.

Normal PGC behavior should come from the always-on profile. Use these references only when the current task needs deeper procedure than the profile should keep in always-loaded context.

## Load strategy

Default to `AGENTS.md` D1-D7. Load one targeted reference when a trigger matches. Load a second only when the task spans two distinct failure modes. Do not load more unless the user explicitly asks for deeper review.

## Reference router

| Trigger | Reference |
| --- | --- |
| Ambiguous, vague, contradictory, emotional, or previously misread request | [semantic-understanding.md](references/semantic-understanding.md) |
| Underspecified or confused input where recovered intent would materially change the answer, or explicit grill-me / exploratory interrogation request | [strong-understanding.md](references/strong-understanding.md) |
| Concept precision, decision criteria, reasoning depth, output shape, or logic-preserving clarity | [reasoning-and-output.md](references/reasoning-and-output.md) |
| Code, commands, files, deployment, debugging, CI, migrations, or scripts | [technical-execution.md](references/technical-execution.md) |
| Current state, file/config/version checks, tool choice, external verification, or validation evidence | [tool-action-strategy.md](references/tool-action-strategy.md) |
| User correction, direction change, rejected assumption, long-context drift, or recovery | [multiturn-recovery.md](references/multiturn-recovery.md) |

## Expected behavior change

After loading a reference, apply its procedure to the current task and return to the smallest useful output. Do not summarize the reference unless the user asks for the reference itself.

## Boundaries

- This pack is text-only.
- It contains no executable code, install hook, network behavior, credentials, or runtime dependency.
- It is not a client-specific adapter.
- It should not override higher-priority safety, user, project, or task-specific instructions.
