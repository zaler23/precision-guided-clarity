---
name: precision-guided-clarity
metadata:
  version: 1.4.0
  scope: generic
  runtime: none
  client_specific: false
  role: supplemental_appendix_index
description: "Supplemental appendix index for Precision-Guided Clarity. AGENTS.md is the complete runtime profile; these files are for maintenance, conformance review, and explicit inspection, not for task routing or prompt branching."
---

# Precision-Guided Clarity Appendices

This directory is supplemental. Normal PGC behavior comes from the single core in `AGENTS.md`.

Do not preload this directory, route ordinary user requests through it, or paste all appendices into a prompt. Use these files only when maintaining the project, auditing conformance, comparing versions, or when the user explicitly asks to inspect PGC internals.

## Appendix index

| File | Purpose |
|---|---|
| [semantic-understanding.md](references/semantic-understanding.md) | Explains ambiguity, weak wording, and intent recovery principles. |
| [strong-understanding.md](references/strong-understanding.md) | Explains deep weak-input recovery, exploratory interrogation boundaries, and embedded cognition. |
| [reasoning-and-output.md](references/reasoning-and-output.md) | Explains decision criteria, output shape, statement types, and logic-preserving clarity. |
| [technical-execution.md](references/technical-execution.md) | Explains reliable technical execution, validation, and outcome-bounded technical initiative. |
| [tool-action-strategy.md](references/tool-action-strategy.md) | Explains state inspection, tool choice, validation evidence, and side-effect sequencing. |
| [multiturn-recovery.md](references/multiturn-recovery.md) | Explains correction handling, drift recovery, and multi-turn state cleanup. |

## Boundary

- `AGENTS.md` is the runtime profile.
- These appendices are text-only and non-executable.
- They are not model-specific, client-specific, or a replacement for task-specific tools and skills.
- They should not override higher-priority user, project, or task-specific instructions.
