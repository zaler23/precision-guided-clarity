---
name: precision-guided-clarity
description: "Optional deep workflow for Precision-Guided Clarity tasks: logic-preserving rewrites, ambiguity triage, correction recovery, context compression, state-aware execution, and high-confidence documentation edits. Not required for normal PGC style when the PGC profile is already installed."
metadata:
  version: 1.0
---

# Precision-Guided Clarity Skill

This skill is now the optional deep-workflow companion to the Precision-Guided Clarity profile.

Normal PGC behavior should come from the always-on profile, such as `AGENTS.md` or your agent's equivalent instruction surface. Use this skill only when the task needs deeper procedure than the profile should keep in the global context.

## Use for

- logic-preserving rewrite or simplification;
- ambiguity triage;
- correction recovery after a wrong assumption;
- stateful technical execution;
- context compression or long-thread recovery;
- release-quality documentation pass.

## Do not use for

- simple Q&A;
- ordinary direct answers already covered by the profile;
- project conventions that belong in project-specific instructions;
- tasks better handled by a more specific skill.

## Reference routing

Load at most two references unless the task clearly needs more.

| Need | Reference |
| --- | --- |
| Ambiguous, vague, contradictory, or emotional request | [semantic-understanding.md](references/semantic-understanding.md) |
| Concept precision, logic-preserving clarity, output depth, decision criteria | [reasoning-and-output.md](references/reasoning-and-output.md) |
| Commands, files, deployments, debugging, CI, migrations | [technical-execution.md](references/technical-execution.md) |
| Current state, file/config/version checks, validation evidence | [tool-action-strategy.md](references/tool-action-strategy.md) |
| User correction, direction change, long-context drift | [multiturn-recovery.md](references/multiturn-recovery.md) |

## Operating rule

Make the profile's light behavior automatic and this skill's heavy behavior available. Do not duplicate long reference content into always-loaded instructions.
