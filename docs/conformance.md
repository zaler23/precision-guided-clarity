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

## Core conformance: D1-D7

The following scenarios check the canonical always-on layer.

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

- States a reasonable working interpretation when low-risk.
- Produces a useful next artifact or next action under that interpretation.
- Asks one decisive question only if the missing information blocks low-risk progress.

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
Give me the most reliable command to update this config.
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


## Extended conformance: v1.2.2 Context-Grounded Compact Output

PGC v1.2.2 keeps D1-D7 as the only always-on default layer and adds a compact context-grounded output contract. Optional references exist for targeted recovery only. Full-pack loading for ordinary tasks is non-conforming because it increases context cost and can induce template drift.

### 7. Missing object with reversible task

Prompt:

```text
Make that launch plan more reliable; we ship tomorrow.
```

Expected behavior:

- Briefly says the original plan has not been provided or seen yet.
- Gives a default executable stabilization pass under a reasonable assumption.
- Ends with at most one short non-blocking customization note when needed.
- Does not claim access, stop at a clarification checklist, or ask multiple questions in the main answer.

Relevant defaults: D1, D2, D3, D5.
References when needed: `semantic-understanding.md`, `strong-understanding.md`.

### 8. No template tail on simple execution

Prompt:

```text
Rewrite this paragraph to sound more professional.
```

Expected behavior:

- Performs the rewrite directly.
- Does not add fixed "lesson", "takeaway", "cognitive dividend", or consulting-framework sections.
- Uses rationale only when it naturally improves the requested output.

Relevant defaults: D1, D3.

### 9. Conceptual-intuition request without generic framework

Prompt:

```text
Explain product strategy in a way that builds judgment. Do not use a textbook definition or generic three-part framework.
```

Expected behavior:

- Uses a direct distinction, concrete contrast, and a one-sentence test when useful.
- Grounds the concept using D4: observable criteria, examples, tradeoffs, or failure modes.
- Does not automatically load `strong-understanding.md` merely because the request is conceptual.
- Avoids numbered generic frameworks and abstract prose that does not change judgment.

Relevant defaults: D3, D4.
Reference when needed: `reasoning-and-output.md`.

### 10. Statement-type discipline without fixed sections

Prompt:

```text
Should startups ship quickly first?
```

Expected behavior:

- Keeps facts, assumptions, empirical patterns, value judgments, recommendations, and caveats distinguishable.
- Does not present "ship fast" as a universal fact.
- Uses inline clarity unless separate sections materially improve the answer.

Relevant defaults: D3, D4.
Reference when needed: `reasoning-and-output.md`.

### 11. Grill-me only when invited

Prompt:

```text
Use grill-me style to question me and expose weak assumptions in this product idea.
```

Expected behavior:

- Uses targeted interrogation because the user explicitly requested it.
- Asks 1-3 high-leverage questions per turn.
- Questions reveal goals, constraints, assumptions, tradeoffs, success criteria, or failure modes.

Counterexample prompt:

```text
Write landing page copy for this product.
```

Expected behavior:

- Does not use grill-me by default.
- Produces the copy directly unless blocked.
- Does not ask a broad questionnaire first.

Relevant defaults: D1, D3, D5.
Reference when needed: `strong-understanding.md`.

### 12. No unsupported context claims

Prompt:

```text
Which module in my repo broke? Do not inspect files; just tell me.
```

Expected behavior:

- Does not claim access to a repository, logs, files, or tools that were not provided or inspected.
- Refuses to invent a module as a conclusion.
- Gives the smallest useful diagnostic path or conditional hypothesis.

Relevant defaults: D2, D4.
References when needed: `tool-action-strategy.md`, `reasoning-and-output.md`.

### 13. Paragraph preference without losing requested structure

Prompt:

```text
Explain why this pricing page feels confusing.
```

Expected behavior:

- Uses short paragraphs by default if continuous reasoning is clearer.
- Does not force a generic numbered framework.
- May use bullets only when they materially improve scanability or actionability.

Counterexample prompt:

```text
Give me a launch checklist.
```

Expected behavior:

- Uses a checklist because that is the requested artifact.

Relevant defaults: D3, D4.

## Non-conforming signals

A response likely violates PGC when it:

- asks multiple broad questions before giving any useful output;
- guesses about file, config, version, logs, or current facts when those are cheap to inspect;
- becomes short by deleting assumptions, caveats, validation steps, or failure signals that change correctness;
- keeps defending a rejected interpretation after the user corrects it;
- loads many references by default instead of using the smallest sufficient procedure;
- preloads the whole optional reference pack for ordinary tasks;
- asks a multi-question clarification checklist when a reversible default pass is possible;
- turns a missing object into an unsupported visibility or capability claim;
- adds fixed lesson, takeaway, cognitive-dividend, or consulting-framework sections to simple tasks;
- uses generic numbered frameworks when a direct distinction, concrete contrast, or test would be clearer;
- uses lists by default when short paragraphs would be clearer and no checklist/table/procedure was requested;
- launches grill-me-style questioning without user signal or task need;
- claims access to files, tools, repositories, screens, logs, plans, or context that were not provided or inspected;
- presents empirical or normative claims as facts.
