# Context management

PGC v1.2.0 separates always-on behavior from optional depth.

## Always loaded

The root `AGENTS.md` is the canonical always-loaded PGC profile. If your agent uses a different instruction surface, copy or merge the same content there.

It contains seven defaults:

- D1 Direct output first.
- D2 Inspect narrow state before guessing.
- D3 Use minimal sufficient depth.
- D4 Preserve logic while simplifying wording.
- D5 Ask one decisive question only when blocked.
- D6 Recover cleanly from corrections.
- D7 Manage context progressively.

This always-loaded layer should stay short enough to audit quickly and to coexist with project-specific or task-specific instructions.

## Optional depth

Use the optional `precision-guided-clarity` reference pack only when the task needs deeper procedure, such as:

- ambiguity triage or semantic mismatch;
- strong understanding for underspecified or confused input where recovered intent would materially change the answer, or explicit grill-me / exploratory interrogation requests;
- concept precision, decision criteria, or output shape;
- technical execution with commands, files, deployment, CI, migrations, or scripts;
- tool choice, current-state inspection, or validation evidence;
- correction recovery, direction change, or long-context drift.

Load one targeted reference by default. Load a second only when the task spans two distinct failure modes. Do not load more unless the user explicitly asks for deeper review.

## Rule

Make the light behavior automatic and the heavy behavior available. Strong understanding should shape normal answers lightly when useful; deep interrogation or teaching remains opt-in or narrowly reference-triggered.

Do not copy long reference content into the always-loaded profile. Doing so increases every session's context cost and weakens the purpose of profile-first design.
