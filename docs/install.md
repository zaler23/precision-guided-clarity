# Install

Precision-Guided Clarity is an agent-agnostic operating profile. The primary artifact is `AGENTS.md`.

## Generic install

Copy or merge the contents of `AGENTS.md` into your agent's global or project instruction surface.

Use this rule when integrating it with any agent:

```text
Load the Precision-Guided Clarity profile as a low-level operating style. Do not let it override higher-priority safety, user, project, or task-specific instructions.
```

If your agent supports `AGENTS.md`, place or merge the root `AGENTS.md` where that agent expects global or project instructions.

## Codex adapter

For Codex CLI and standard Codex runs, one common path is `~/.codex/AGENTS.md`.

Safe copy with backup:

```bash
set -e
mkdir -p "${HOME}/.codex"
if [ -f "${HOME}/.codex/AGENTS.md" ]; then
  cp "${HOME}/.codex/AGENTS.md" "${HOME}/.codex/AGENTS.md.bak.$(date +%Y%m%d%H%M%S)"
fi
cp AGENTS.md "${HOME}/.codex/AGENTS.md"
```

If you already maintain global guidance, merge the marked block manually instead of overwriting the file.

## Codex temporary override

Use `profiles/codex-AGENTS.override.md` only when you intentionally want to mask normal Codex global guidance:

```bash
set -e
mkdir -p "${HOME}/.codex"
cp profiles/codex-AGENTS.override.md "${HOME}/.codex/AGENTS.override.md"
```

Remove it to restore normal global guidance:

```bash
rm "${HOME}/.codex/AGENTS.override.md"
```

## Codex Desktop with `model_instructions_file`

If your Codex Desktop config already uses `model_instructions_file`, append the Codex Desktop adapter fragment into that configured file. Back it up first.

```bash
set -e
DESKTOP_INSTRUCTIONS="${HOME}/.codex/desktop-instructions.md"
cp "${DESKTOP_INSTRUCTIONS}" "${DESKTOP_INSTRUCTIONS}.bak.$(date +%Y%m%d%H%M%S)"
cat profiles/codex-desktop-instructions.append.md >> "${DESKTOP_INSTRUCTIONS}"
```

If your configured file is somewhere else, replace `DESKTOP_INSTRUCTIONS` with that absolute path.

Do not point `model_instructions_file` directly at the short PGC profile unless you intentionally want to replace the full instruction base.

## Optional Codex named profile

Append `profiles/codex-config.profile.toml` into `~/.codex/config.toml`, then run:

```bash
codex --profile pgc "Summarize the active Precision-Guided Clarity instructions."
```

The named config profile is optional. `AGENTS.md` remains the primary instruction carrier.

## Optional skill compatibility

The `precision-guided-clarity/` directory is available for agents that support on-demand skills or reusable instruction bundles.

For Codex-compatible skill directories:

```bash
set -e
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
rm -rf "${CODEX_HOME:-$HOME/.codex}/skills/precision-guided-clarity"
cp -R precision-guided-clarity "${CODEX_HOME:-$HOME/.codex}/skills/"
```

## Update or uninstall

PGC uses visible marker blocks so it can be updated or removed without guessing.

If PGC was merged into an instruction file, remove the block between:

```text
<!-- BEGIN precision-guided-clarity v1.0 -->
<!-- END precision-guided-clarity v1.0 -->
```

For the optional Codex CLI profile, remove the `[profiles.pgc]` block from `~/.codex/config.toml`.

For the optional skill, remove the copied skill directory. In a Codex-compatible location:

```bash
rm -rf "${CODEX_HOME:-$HOME/.codex}/skills/precision-guided-clarity"
```

Restart your agent or start a new session after changing global guidance or skills.
