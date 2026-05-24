# Technical Execution

Use for code, commands, files, deployment, automation, debugging, servers, CI/CD, migrations, or scripts.

## Contract

Unless the user asks for explanation only, provide:

1. Relevant environment assumptions
2. One complete command group, patch, or script
3. Validation command or expected output
4. Most likely failure point
5. Rollback or recovery note when the change is hard to reverse

## Inspect First

When local tools are available and the task depends on actual machine state, inspect the relevant state before final commands or edits. This is a baseline rule from `SKILL.md`, not optional extra guidance.

Check only what matters:

- target files and current directory
- installed tool versions
- active config paths
- service status or ports
- existing generated artifacts

Do not run broad scans when a narrow check is enough.

For cross-tool inspection, current-fact verification, file state discovery, command results, generated artifacts, service checks, validation workflow, or operational anchors, use `references/tool-action-strategy.md`.

If a task is both technical and high risk, inspect state first. After inspection, preserve the decision criterion, rollback boundary, access boundary, migration consequence, or evidence limitation that still determines the answer.

## Command Style

Prefer one complete executable block:

```bash
set -e
# commands here
```

over scattered one-line fragments.

For destructive or hard-to-reverse file operations, show the target path clearly and include a verification or recovery step.

## Missing Information

Ask before execution only when missing information would cause wrong environment changes, overwritten files, wrong target selection, or non-recoverable output.

Otherwise assume a reasonable default, state it, and provide a usable command.

## Validation Examples

Choose validation based on the task:

```bash
command -v tool
tool --version
curl -I http://localhost:PORT
python -m pytest
npm test
service status name
```

For file edits, verify by reading the changed file, running the relevant test, or checking the generated artifact.

## Failure and Recovery

Name the most likely failure point before the user hits it.

Common causes by category - environment, data state, permissions:

- Environment: wrong runtime version, wrong working directory, missing environment variable, port conflict
- Data state: stale generated artifact, migration applied to the wrong database
- Permissions: missing file, directory, network, or account permission

If the change is risky, include a rollback, backup, dry run, or restore path.
