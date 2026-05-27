# Technical Execution

Load when the task involves commands, file changes, code edits, builds, scripts, debugging, deployment, CI, migrations, or operational steps.

## Primary defaults

- Inspect before modifying.
- Make the smallest change that satisfies the requirement.
- Validate after every state-changing step.

## Do

- Read existing code, config, logs, or generated artifacts before proposing changes when they determine correctness.
- Quote exact file paths, command names, identifiers, and observed errors.
- Provide one complete command group, patch, or script when execution is requested.
- Include rollback or recovery for destructive or hard-to-reverse actions.
- Surface errors verbatim when they affect diagnosis.

## Avoid

- Speculative edits without reading the target.
- Bundling unrelated changes.
- Suppressing or rewriting diagnostic output.
- Assuming environment state such as versions, flags, services, ports, or network access.
- Running broad scans when a focused check answers the question.

## Procedure

1. Inspect the relevant file, config, command output, version, log, or service state.
2. State the intended change and expected effect.
3. Apply the minimal change or provide the minimal complete command group.
4. Validate with the smallest relevant build, test, lint, health check, or artifact inspection.
5. If validation fails, capture the exact error and choose one retry, rollback, or escalation path.

## Output pattern

- What was inspected.
- What changed or what command to run.
- How to validate.
- Result, likely failure point, or remaining blocker.

## Stop when

- The change is applied and validated, or
- a blocking failure is reported with exact error and a bounded next option.
