# precision-guided-clarity

[简体中文](README.zh-CN.md)

Precision-Guided Clarity is a compact, generic instruction profile for AI agents. It is instruction-only: no runtime, no MCP service, no hooks, no client-specific adapter.

PGC is a lightweight behavior contract and cognitive-shaping core, not a capability upgrade. Its job is to keep an agent useful under ambiguity: do not blindly obey flawed wording, do not stall when a useful partial result exists, do not ignore open-ended scope, do not invent unseen context, and do not turn answers into teaching templates. When context is missing, say so before relying on it; when low-risk progress is possible, make the bounded useful move. The user should quietly gain sharper judgment and transferable intuition from the answer itself.

**Version:** 1.4.2
**Runtime artifact:** `AGENTS.md`
**Supplemental artifacts:** `precision-guided-clarity/` and `docs/`, for maintainers and conformance review only

## Design goal

PGC keeps one minimal core instead of branching into prompt modes. The profile helps an agent:

- start with the answer, patch, command, recommendation, or one blocker question;
- infer the user's likely goal, bottleneck, and outcome risk from visible context, then act inside the available evidence;
- state missing referenced objects before relying on them, while still giving a practical default pass when the work is reversible;
- preserve scope markers such as all, any, including, etc., similar, other, 等, and 之类, instead of shrinking open-ended requests to only named examples;
- preserve the user's real goal over flawed literal wording;
- take the most reliable useful reversible step when exact execution is not yet justified;
- provide a default usable pass for vague but reversible work before mentioning missing details;
- inspect the narrowest relevant state before guessing when correctness depends on state;
- avoid unsupported claims of seeing files, logs, screens, tools, codebases, or other missing context;
- embed one strong cognitive anchor when it improves the answer, without expanding it into a framework;
- preserve logic while simplifying wording;
- ask one decisive question only when blocked;
- default to tight natural prose and use lists or tables only when they materially improve the result, not merely to look organized.

## What is included

- `AGENTS.md` is the complete runtime profile.
- `precision-guided-clarity/SKILL.md` is a supplemental appendix index, not a routing layer.
- `precision-guided-clarity/references/*.md` contains explanatory appendices for maintainers, audits, and compatibility review.
- `docs/` contains installation, context, and conformance notes.

The supplemental files are not required for ordinary prompting. Do not preload them to make PGC work. If a host system can expose them, treat them as reference material for explicit review, not as task routers.

## Generic install

Copy or merge the contents of `AGENTS.md` into the instruction surface your agent already supports, such as a system prompt, project instruction, `AGENTS.md`-style file, or custom instruction field.

Recommended integration rule:

```text
Load Precision-Guided Clarity as a low-level operating style. Use AGENTS.md as the complete PGC runtime profile. Do not add extra PGC routing layers unless a user explicitly asks to inspect or audit the PGC documents.
```

## Update or remove

PGC uses visible marker blocks so it can be updated or removed without guessing. Remove the block between:

```text
<!-- BEGIN precision-guided-clarity v1.4.2 -->
<!-- END precision-guided-clarity v1.4.2 -->
```

Restart your agent or start a new session after changing global or project-level instructions.

## Project structure

```text
AGENTS.md                          # complete runtime profile
README.md                          # English overview
README.zh-CN.md                    # Simplified Chinese overview
docs/install.md                    # generic installation guide
docs/context-management.md         # single-core context guidance
docs/conformance.md                # manual behavior checks
precision-guided-clarity/          # supplemental appendices, not runtime routing
```

## Distribution

Use the source repository as the distribution format. Clone the repository and verify the commit hash when you need reproducibility.

This project does not provide custom zip, tar, checksum, installer, or executable release artifacts.

## License

MIT. See `LICENSE`.
