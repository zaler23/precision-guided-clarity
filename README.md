# precision-guided-clarity

[简体中文](README.zh-CN.md)

Precision-Guided Clarity is a generic instruction profile for AI agents. Copy or merge it into any compatible agent instruction surface, such as a system prompt, project instructions, `AGENTS.md`-style file, or custom instruction field. It is not a client-specific adapter package.

PGC is a lightweight behavior contract, not a capability upgrade. Its core value is a judgment-guided cognitive core: useful answers should help the user build sharper judgment, transferable intuition, and more precise mental models by silently diagnosing the current bottleneck and acting on it without adding cognitive overhead. On frontier RLHF models, many defaults already overlap with PGC; its practical value is reducing behavior drift and making edge-case preferences explicit around ambiguity, context grounding, correction, over-teaching, template drift, and implicit cognition-building.

**Version:** 1.2.5
**Primary artifact:** `AGENTS.md`
**On-demand artifact:** `precision-guided-clarity/` reference pack for compatible skill or reference systems

## Design goal

PGC prioritizes useful agent behavior first, then keeps the implementation compact, copyable, and low-token. The profile helps an agent:

- start with the answer, command, patch, recommendation, or one blocking question;
- silently infer the user's current bottleneck from the request and visible context, then act on that inference;
- shape answers so users quietly build judgment, transferable intuition, and precise mental models;
- include one high-leverage cognitive anchor only when it improves the result, and prefer one strong anchor over a full framework;
- balance openness and rigor by judgment: explore when it creates better options, converge when the user needs a decision, action, correction, or boundary;
- add depth only when it changes the user's decision, action, or understanding;
- inspect the narrowest relevant state before guessing;
- use the smallest complete answer that preserves correctness;
- simplify wording without deleting assumptions, criteria, causal links, mechanisms, caveats, validation steps, or failure signals;
- ask one decisive clarification question only when blocked;
- deliver a useful default pass under a stated assumption before requesting missing detail when ambiguity is reversible;
- avoid implying access to missing objects, files, tools, logs, screens, plans, or codebases;
- avoid fixed teaching, takeaway, cognitive-dividend, task-category, or consulting-framework tails unless requested;
- default to tight natural prose, using lists, numbered steps, or tables only when they materially improve actionability, exact comparison, verification, or logic preservation;
- recover from corrections by replacing the broken assumption;
- keep always-loaded context small and load deeper references only when needed.

## What is included

- `AGENTS.md` is the canonical always-on profile.
- `precision-guided-clarity/SKILL.md` is an on-demand routing index for compatible reference or skill systems.
- `precision-guided-clarity/references/*.md` contains deeper guidance for ambiguity handling, strong understanding, reasoning, technical execution, tool-mediated work, and multi-turn recovery.
- `docs/` contains generic installation, context-management, and conformance notes.

This repository does not ship client-specific configuration files, runtime code, install hooks, automation scripts, or custom release archives.

## Generic install

Copy or merge the contents of `AGENTS.md` into the instruction surface your agent already supports.

Recommended integration rule:

```text
Load the Precision-Guided Clarity profile as a low-level operating style. Do not let it override higher-priority user, project, or task-specific instructions.
```

If your agent supports project instruction files, place or merge the root `AGENTS.md` where that agent expects project or global instructions.

## On-demand reference pack

The `precision-guided-clarity/` directory is part of the PGC specification, but it should be loaded on demand. Use it when your agent can read local references or load on-demand skills.

For compatible systems, copy the directory into the location that system uses for reference packs or skills. If you move it to a different path, update the reference paths in `AGENTS.md` or keep the same relative layout.

The always-on cognitive/intuition layer lives in `AGENTS.md`. References are loaded only when the task triggers deeper procedure. Do not paste or preload the full reference pack for ordinary tasks; that increases context cost and can induce template drift.

## Update or remove

PGC uses visible marker blocks so it can be updated or removed without guessing. Remove the block between:

```text
<!-- BEGIN precision-guided-clarity v1.2.5 -->
<!-- END precision-guided-clarity v1.2.5 -->
```

If you installed the on-demand reference pack, remove the copied `precision-guided-clarity` directory from the location where you placed it.

Restart your agent or start a new session after changing global or project-level instructions.

## Project structure

```text
AGENTS.md                          # canonical always-on generic profile
README.md                          # English overview
README.zh-CN.md                    # Simplified Chinese overview
docs/install.md                    # generic installation guide
docs/context-management.md         # always-loaded vs on-demand reference strategy
docs/conformance.md                # manual behavior checks
precision-guided-clarity/          # on-demand core reference pack
```

## Distribution

Use the source repository as the distribution format. Clone the repository and verify the commit hash when you need reproducibility.

This project does not provide custom zip, tar, checksum, installer, or executable release artifacts.

## License

MIT. See `LICENSE`.
