# precision-guided-clarity

[简体中文](README.zh-CN.md)

A tiny agent-agnostic operating profile for agentic work: direct output, narrow state inspection, logic-preserving clarity, minimal sufficient depth, clean correction recovery, and progressive context management.

**Version:** 1.0  
**Primary artifact:** `AGENTS.md`  
**Optional artifact:** `precision-guided-clarity/` skill for compatible skill systems

## What it does

Precision-Guided Clarity helps an agent:

- start with the answer, command, patch, recommendation, or one blocking question;
- inspect the narrowest relevant state before guessing;
- use the smallest complete answer that preserves correctness;
- simplify wording without deleting assumptions, criteria, causal links, mechanisms, caveats, validation steps, or failure signals;
- ask one decisive clarification question only when blocked;
- recover from corrections by replacing the broken assumption;
- keep always-loaded context small and load deeper guidance only when needed.

## Who it is for

Use it with any agent or assistant that supports one of these instruction surfaces:

- global instructions;
- project instructions;
- `AGENTS.md`-style instruction files;
- custom system/profile prompts;
- skill-style on-demand instruction bundles.

This project is not tied to a single agent runtime. Codex-specific files are provided only as optional adapters.

## Generic install

Use the contents of `AGENTS.md` as the always-on profile in your agent's global or project instruction surface.

Recommended rule:

```text
Load the Precision-Guided Clarity profile as a low-level operating style. Do not let it override higher-priority safety, user, project, or task-specific instructions.
```

If your agent supports `AGENTS.md`, place or merge the root `AGENTS.md` where that agent expects project or global agent instructions.

## Codex adapter install

For Codex CLI and standard Codex runs, one common path is `~/.codex/AGENTS.md`:

```bash
set -e
mkdir -p "${HOME}/.codex"
if [ -f "${HOME}/.codex/AGENTS.md" ]; then
  cp "${HOME}/.codex/AGENTS.md" "${HOME}/.codex/AGENTS.md.bak.$(date +%Y%m%d%H%M%S)"
fi
cp AGENTS.md "${HOME}/.codex/AGENTS.md"
```

If you already maintain global instructions, merge the marked block manually instead of overwriting the file.

For Codex Desktop setups that already use `model_instructions_file`, append the Codex Desktop adapter fragment into the configured file:

```bash
set -e
DESKTOP_INSTRUCTIONS="${HOME}/.codex/desktop-instructions.md"
cp "${DESKTOP_INSTRUCTIONS}" "${DESKTOP_INSTRUCTIONS}.bak.$(date +%Y%m%d%H%M%S)"
cat profiles/codex-desktop-instructions.append.md >> "${DESKTOP_INSTRUCTIONS}"
```

`profiles/codex-config.profile.toml` is an optional Codex config snippet for users who want a named profile.

## Optional skill compatibility

The `precision-guided-clarity/` directory is an optional skill-style artifact for agents that support on-demand skills or reusable instruction bundles.

For Codex-compatible skill directories:

```bash
set -e
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
rm -rf "${CODEX_HOME:-$HOME/.codex}/skills/precision-guided-clarity"
cp -R precision-guided-clarity "${CODEX_HOME:-$HOME/.codex}/skills/"
```

The skill is not the primary carrier. Use it only for logic-preserving rewrites, ambiguity triage, correction recovery, context compression, state-aware execution, or release-quality documentation passes.

## Update or remove

Remove the marked PGC block from the instruction file where you installed it. If you installed the optional Codex profile, remove `[profiles.pgc]` from your Codex config. If you installed the optional skill, remove the copied `precision-guided-clarity` skill directory.

## Project structure

```text
AGENTS.md                                     # canonical always-on profile
profiles/codex-AGENTS.override.md            # optional Codex override adapter
profiles/codex-desktop-instructions.append.md# optional Codex Desktop append adapter
profiles/codex-config.profile.toml           # optional Codex config snippet
docs/install.md                              # generic install and adapter details
docs/context-management.md                   # always-loaded vs optional strategy
precision-guided-clarity/                    # optional compatibility skill
```

## Security posture

This project is instruction-only. It contains no runtime executables, install hooks, remote fetch logic, bundled credentials, or pre-authorized tool configuration.

## License

MIT. See `LICENSE`.
