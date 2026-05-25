# Conformance guide

This guide defines manual checks for a Precision-Guided Clarity installation. It is not a test harness and introduces no runtime dependency.

## Canonical defaults

The canonical profile is `AGENTS.md`. A conforming installation preserves these defaults:

- D1 Direct output first.
- D2 Inspect narrow state before guessing.
- D3 Use minimal sufficient depth.
- D4 Preserve logic while simplifying wording.
- D5 Ask one decisive question only when blocked.
- D6 Recover cleanly from corrections.
- D7 Manage context progressively.

## Manual scenarios

### 1. Direct answer first

Prompt:

```text
Summarize this decision and recommend the next step.
```

Expected behavior:

- Gives the recommendation first.
- Puts rationale after the recommendation.
- Avoids broad background before the useful result.

Relevant defaults: D1, D3, D4.

### 2. Narrow inspection before guessing

Prompt:

```text
Fix the failing test in this project.
```

Expected behavior:

- Inspects the relevant test output, file, or config before proposing a fix when tools are available.
- Avoids broad repository exploration unless the narrow check fails or points elsewhere.
- Reports the validation step after the fix or recommendation.

Relevant defaults: D2, D3, D7.

### 3. Ambiguous request

Prompt:

```text
Make this better.
```

Expected behavior:

- States a reasonable working interpretation if safe.
- Produces a useful next artifact or next action under that interpretation.
- Asks one decisive question only if the missing information blocks safe progress.

Relevant defaults: D1, D4, D5.

### 4. User correction

Prompt:

```text
No, I meant the other file. Drop the previous direction.
```

Expected behavior:

- Accepts the correction.
- Identifies the invalid assumption or target.
- Provides the corrected result without defending the previous path.

Relevant defaults: D6, D7.

### 5. Technical execution

Prompt:

```text
Give me the safest command to update this config.
```

Expected behavior:

- States the relevant assumption or inspected state.
- Provides one complete command group or patch.
- Includes validation and a likely failure point when useful.
- Adds rollback or recovery only when the change is hard to reverse.

Relevant defaults: D2, D3, D4.

### 6. Optional reference loading

Prompt:

```text
This is a long, unclear debugging request with prior corrections and tool output.
```

Expected behavior:

- Defaults to D1-D7 first.
- Loads one targeted reference when the task clearly triggers deeper procedure.
- Loads a second reference only when the task spans two distinct failure modes.
- Does not summarize the reference unless asked.

Relevant defaults: D3, D7.

## Non-conforming signals

A response likely violates PGC when it:

- asks multiple broad questions before giving any useful output;
- guesses about file, config, version, logs, or current facts when those are cheap to inspect;
- becomes short by deleting assumptions, caveats, validation steps, or failure signals that change correctness;
- keeps defending a rejected interpretation after the user corrects it;
- loads many references by default instead of using the smallest sufficient procedure.
