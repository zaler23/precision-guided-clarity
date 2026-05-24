# Tool Action Strategy

Use when correctness depends on current reality, actual environment state, external facts, file contents, generated artifacts, command results, service status, or validation evidence.

## Baseline And Full Strategy

`SKILL.md` carries the baseline rule: inspect the narrowest source of truth before guessing when state controls correctness. Load this reference when the task needs a tool sequence, validation workflow, destructive-change check, external verification path, or state-discovery plan.

The baseline prevents cold-start guessing. This file controls how to inspect, validate, and report without turning tool use into a broad scan.

## Core Rule

Do not guess when the relevant state is cheap to inspect and the answer, edit, command, or recommendation depends on that state.

Tool use should reduce uncertainty before advising, editing, executing, or concluding. It should not become a broad scan or a substitute for judgment.

## When To Use Tools

Use tools before final advice or execution when the task depends on:

- current public facts, product behavior, schedules, prices, rules, standards, or recent changes
- actual files, repository structure, configs, generated artifacts, logs, or test output
- installed versions, package managers, runtime behavior, service status, ports, or health checks
- exact target selection for edits, deletion, migration, deployment, or rollback
- validation evidence for a generated document, spreadsheet, slide deck, patch, or script

Do not use tools merely to decorate an answer when the answer is stable, low-risk, and already knowable.

## Inspection Order

Inspect the narrowest source of truth first:

1. Identify the target that controls correctness.
2. Inspect the target or active configuration, not every nearby file.
3. Check prerequisites only when they affect the next action.
4. Make the smallest useful edit, recommendation, or command group.
5. Validate with the smallest relevant check before broader tests.

Examples of narrow checks:

```text
read the target file before patching it
list the expected output directory before overwriting generated artifacts
check the active config path before editing a template
run the one relevant test before the full suite
check the port or health endpoint before rewriting deployment logic
verify the current rule or version before recommending version-specific behavior
```

## State Before Abstraction

For technical risk tasks, inspect concrete state before adding abstract risk analysis.

Prefer:

```text
I checked X. The blocking fact is Y. Because Y affects Z, the safe next action is A.
```

over:

```text
There are several possible risks depending on your environment.
```

After inspection, add only the decision criterion, rollback boundary, access boundary, migration consequence, or evidence limitation that still determines the answer.

## Tool Choice

Choose the lightest available tool that can answer the state question:

- File state: list paths, read the target file, or inspect the generated artifact.
- Runtime state: check versions, package metadata, service status, logs, ports, or health endpoints.
- External facts: search or open authoritative sources; cite or mark uncertainty when facts may have changed.
- Validation: run the smallest relevant command, parse the output, and report only what affects the answer.

Do not expose secrets. Inspect environment variable names or config keys when useful, but avoid printing values unless the user explicitly provides safe test values.

## Destructive Or Hard-To-Reverse Work

Before deletion, migration, overwrite, deployment, permission change, or bulk edit:

1. Confirm or inspect the exact target.
2. Prefer a dry run, backup, restore path, or reversible step.
3. Show the target clearly before applying the change.
4. Validate the result.

If the target is missing and a wrong guess could damage state, ask one decisive question for the target identifier or path.

## If Tools Are Unavailable

If tool access is unavailable or insufficient:

1. State the assumption.
2. Mark the unverified part.
3. Give the exact verification command, query, or check.
4. Give the conservative next step.

Do not turn lack of tool access into a long disclaimer. Give the best usable path with clear verification.

## Operational Anchors

For stateful, tool-mediated, multi-step, destructive, or hard-to-reverse work, expose one short operational anchor when it helps prevent drift or build trust.

The anchor should include:

1. the source of truth to inspect
2. the action scope
3. the validation target

Good anchors:

```text
I will inspect the active config, patch only that file, then run the focused startup check.
I need the target path before deletion; after that I will dry-run the cleanup and show the affected files.
```

Weak anchors:

```text
I will think through the internal categories first and then decide what to do.
```

The anchor is a user-facing action contract. It should help the user understand what will be inspected, changed, and validated.

## Output Discipline

Expose only tool findings that change action, correctness, risk, trust, or validation.

Avoid:

- dumping raw logs when one line matters
- narrating every inspection step
- broad repository scans without a target
- replacing a missing check with generic caveats
- loading more references unless a specific failure requires them
