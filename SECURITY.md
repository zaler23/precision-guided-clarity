# Security

Precision-Guided Clarity is instruction-only.

## Runtime surfaces

Primary profile files:

- `AGENTS.md`
- `profiles/AGENTS.override.md`
- `profiles/desktop-instructions.append.md`
- `profiles/config.profile.toml`

Optional skill files:

- `precision-guided-clarity/SKILL.md`
- `precision-guided-clarity/references/*.md`

The project contains no runtime executables, install hooks, remote fetch logic, bundled credentials, or pre-authorized tool configuration.

## Practical risk

Instruction-only does not mean risk-free. A profile or skill can still influence agent behavior through text. Review the profile and optional skill before adoption.

## Verification checklist

Before using a release archive:

1. Inspect the file tree.
2. Verify the archive checksum when one is provided.
3. Confirm no temporary files, personal paths, or machine-specific traces are included.
4. Confirm the runtime remains instruction-only.
