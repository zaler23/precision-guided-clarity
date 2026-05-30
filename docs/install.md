# Install

PGC v1.4.2 is a single-core instruction profile.

## 1. Copy the runtime profile

Copy or merge `AGENTS.md` into the instruction surface your agent supports:

- system prompt;
- project instructions;
- `AGENTS.md`-style project file;
- custom instruction field.

Do not preload `precision-guided-clarity/` or `docs/` as prompt content for ordinary use.

## 2. Preserve the marker block

PGC is delimited by visible markers:

```text
<!-- BEGIN precision-guided-clarity v1.4.2 -->
...
<!-- END precision-guided-clarity v1.4.2 -->
```

Keep these markers so updates and removal are mechanical.

## 3. Optional supplemental files

You may copy the rest of the repository for documentation, maintenance, and conformance checks:

```text
precision-guided-clarity/
  SKILL.md
  references/
    semantic-understanding.md
    strong-understanding.md
    reasoning-and-output.md
    technical-execution.md
    tool-action-strategy.md
    multiturn-recovery.md
docs/
  context-management.md
  conformance.md
  install.md
```

These files are not a runtime routing layer. Use them only for explicit inspection, audits, or project maintenance.

## 4. Verify

After installation, check that the active runtime prompt contains `AGENTS.md` and does not contain duplicated appendices or multiple PGC versions.
