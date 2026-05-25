# Security

Precision-Guided Clarity is instruction-only.

## Runtime surfaces

Primary profile file:

- `AGENTS.md`

Optional reference files:

- `precision-guided-clarity/SKILL.md`
- `precision-guided-clarity/references/*.md`
- `docs/*.md`

The project contains no runtime executables, install hooks, remote fetch logic, bundled credentials, pre-authorized tool configuration, or client-specific config files.

## Distribution

This project is distributed as source text in the repository. It does not provide custom zip, tar, checksum, installer, binary, or executable release artifacts.

For reproducibility, prefer `git clone` and verify the commit hash you intend to use.

## Practical risk

Instruction-only does not mean risk-free. A profile or reference file can still influence agent behavior through text. Review `AGENTS.md` and the optional reference pack before adoption.

This project does not grant new permissions to an agent. Tool access, sandboxing, network access, file access, and approval behavior remain controlled by the host environment.

## Verification checklist

Before using a revision:

1. Inspect the file tree.
2. Verify the commit hash if reproducibility matters.
3. Confirm no temporary files, personal paths, local maintenance records, archives, or machine-specific traces are included.
4. Confirm the runtime remains instruction-only.
5. Confirm the host agent's tool permissions are configured separately from this profile.
