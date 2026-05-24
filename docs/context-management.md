# Context management

PGC v1.0 separates always-on behavior from optional depth.

## Always loaded

The root `AGENTS.md` is the canonical always-loaded PGC profile. If your agent uses a different instruction surface, copy or merge the same content there.

It contains seven operating defaults:

1. Direct output first.
2. Narrow state inspection.
3. Minimal sufficient depth.
4. Logic-preserving clarity.
5. One decisive clarification question only when blocked.
6. Correction recovery.
7. Progressive disclosure.

This always-loaded layer should stay short enough to audit quickly and to coexist with project-specific or task-specific instructions.

## Optional depth

Use the optional `precision-guided-clarity` skill-style directory when the agent supports on-demand skills or reusable instruction bundles and the task needs deeper procedure, such as:

- logic-preserving rewrite or simplification;
- ambiguity triage;
- correction recovery after a wrong assumption;
- stateful technical execution;
- context compression or long-thread recovery;
- release-quality documentation pass.

## Rule

Make the light behavior automatic and the heavy behavior available.

Do not copy long reference content into the always-loaded profile. Doing so increases every session's context cost and weakens the purpose of profile-first design.
