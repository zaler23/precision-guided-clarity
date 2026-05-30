# Context management

PGC v1.4.2 uses a single-core stable runtime profile.

## Runtime context

Use `AGENTS.md` as the complete PGC instruction surface. If your agent uses another instruction location, copy or merge the same content there.

The runtime core contains:

- Minimal Cognitive Core with bounded initiative, open-ended scope preservation, and explicit missing-context disclosure.
- D1 Direct output first.
- D2 Inspect narrow state before guessing.
- D3 Use minimal sufficient depth.
- D4 Preserve logic while simplifying wording.
- D5 Ask one decisive question only when blocked.
- D6 Recover cleanly from corrections.
- D7 Keep the profile compact.
- Behavior Anchor.

## No PGC routing layer

Do not split requests into separate PGC modes, model branches, or reference-loading paths. Do not add a reference layer for ordinary ambiguity, open-ended scope, explanation, or reasoning. Do not preload the supplemental appendices for ordinary tasks.

This is intentional: recent testing showed that heavier loading and routing can increase cost, template drift, clarification loops, and consulting-style structure. PGC should stay as a small always-on core. Stability comes from the core itself: disclose missing context, make a practical default pass when reversible, protect the user's real goal, and avoid expanding one useful anchor into a framework.

## Supplemental files

`precision-guided-clarity/` and `docs/` are useful for maintainers, audits, and explicit user inspection. They are not required for normal answers.

If a host system exposes those files automatically, treat them as background documentation. Do not let them become another prompt layer unless the user explicitly asks for a PGC audit, comparison, or documentation task.

## Practical rule

Make the light behavior automatic. Keep everything else documentary.
