# Install

Precision-Guided Clarity is a generic instruction profile. The primary artifact is `AGENTS.md`, which carries the core behavior including the judgment-guided cognitive core and D1-D7.

## Generic install

Copy or merge the contents of `AGENTS.md` into the instruction surface your agent already supports.

Use this integration rule:

```text
Load AGENTS.md as the always-on Precision-Guided Clarity profile. Do not preload the on-demand reference pack. Load one targeted reference only when a narrow trigger matches. Do not let PGC override higher-priority user, project, or task-specific instructions.
```

Compatible instruction surfaces may include:

- global instructions;
- project instructions;
- `AGENTS.md`-style instruction files;
- custom system or profile prompts;
- application-specific custom instruction fields.

## On-demand reference pack

The `precision-guided-clarity/` directory is part of the PGC specification, but it should be loaded on demand. Use it only when your agent can read local references or load on-demand skills.

Recommended layout when the agent can read project-relative paths:

```text
AGENTS.md
precision-guided-clarity/
  SKILL.md
  references/
    semantic-understanding.md
    strong-understanding.md
    reasoning-and-output.md
    technical-execution.md
    tool-action-strategy.md
    multiturn-recovery.md
```

If your agent stores references elsewhere, copy the directory to that location and update the paths in `AGENTS.md` if needed.

## Verify installation

Start a new session and ask the agent to summarize the active PGC defaults. A correct installation should mention D1-D7 and the silent-diagnosis judgment-guided cognitive core, and should not claim to have new tool permissions, runtime hooks, or automatic network behavior.

## Update or uninstall

PGC uses visible marker blocks so it can be updated or removed without guessing. Remove the block between:

```text
<!-- BEGIN precision-guided-clarity v1.2.5 -->
<!-- END precision-guided-clarity v1.2.5 -->
```

If you installed the on-demand reference pack, remove the copied `precision-guided-clarity` directory from the location where you placed it.

Restart your agent or start a new session after changing global or project-level instructions.

## Distribution note

Use the source repository as the distribution format. This project does not provide custom package archives, installers, generated checksums, or executable release artifacts.
