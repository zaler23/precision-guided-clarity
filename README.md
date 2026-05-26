# precision-guided-clarity

[简体中文](README.zh-CN.md)

Precision-Guided Clarity is a generic instruction profile for AI agents. Copy or merge it into any compatible agent instruction surface, such as a system prompt, project instructions, `AGENTS.md`-style file, or custom instruction field. It is not a client-specific adapter package.

PGC is designed not only to produce clear answers, but to support strong understanding: answers should help clarify intent, ground important claims, and improve judgment without turning ordinary tasks into lessons.

**Version:** 1.2.0  
**Primary artifact:** `AGENTS.md`  
**Optional artifact:** `precision-guided-clarity/` reference pack for compatible on-demand skill or reference systems

## Design goal

PGC prioritizes useful agent behavior first, then keeps the implementation compact, copyable, and low-token. The profile helps an agent:

- start with the answer, command, patch, recommendation, or one blocking question;
- inspect the narrowest relevant state before guessing;
- use the smallest complete answer that preserves correctness;
- simplify wording without deleting assumptions, criteria, causal links, mechanisms, caveats, validation steps, or failure signals;
- shape answers so important claims are grounded in concrete structure, boundaries, decision rules, or failure modes when useful;
- ask one decisive clarification question only when blocked;
- recover from corrections by replacing the broken assumption;
- keep always-loaded context small and load deeper references only when needed.

## What is included

- `AGENTS.md` is the canonical always-on profile.
- `precision-guided-clarity/SKILL.md` is an optional routing index for compatible reference or skill systems.
- `precision-guided-clarity/references/*.md` contains deeper guidance for ambiguity handling, strong understanding, reasoning, technical execution, tool-mediated work, and multi-turn recovery.
- `docs/` contains generic installation, context-management, and conformance notes.

This repository does not ship client-specific configuration files, runtime code, install hooks, automation scripts, or custom release archives.

## Generic install

Copy or merge the contents of `AGENTS.md` into the instruction surface your agent already supports.

Recommended integration rule:

```text
Load the Precision-Guided Clarity profile as a low-level operating style. Do not let it override higher-priority safety, user, project, or task-specific instructions.
```

If your agent supports project instruction files, place or merge the root `AGENTS.md` where that agent expects project or global instructions.

## Optional reference pack

The `precision-guided-clarity/` directory is optional. Use it only when your agent can read local references or load on-demand skills.

For compatible systems, copy the directory into the location that system uses for reference packs or skills. If you move it to a different path, update the reference paths in `AGENTS.md` or keep the same relative layout.

The reference pack is not the primary carrier. Normal behavior should come from `AGENTS.md`; references are loaded only when the task triggers deeper procedure.

## Update or remove

PGC uses visible marker blocks so it can be updated or removed without guessing. Remove the block between:

```text
<!-- BEGIN precision-guided-clarity v1.2.0 -->
<!-- END precision-guided-clarity v1.2.0 -->
```

If you installed the optional reference pack, remove the copied `precision-guided-clarity` directory from the location where you placed it.

Restart your agent or start a new session after changing global or project-level instructions.

## Project structure

```text
AGENTS.md                          # canonical always-on generic profile
README.md                          # English overview
README.zh-CN.md                    # Simplified Chinese overview
SECURITY.md                        # security posture and verification notes
docs/install.md                    # generic installation guide
docs/context-management.md         # always-loaded vs optional reference strategy
docs/conformance.md                # manual behavior checks
precision-guided-clarity/          # optional reference pack
```

## Distribution

Use the source repository as the distribution format. Clone the repository and verify the commit hash when you need reproducibility.

This project does not provide custom zip, tar, checksum, installer, or executable release artifacts.

## Security posture

This project is instruction-only. It contains no runtime executables, install hooks, remote fetch logic, bundled credentials, or pre-authorized tool configuration.

## License

MIT. See `LICENSE`.
