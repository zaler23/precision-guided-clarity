# Tool and Action Strategy

Appendix purpose: explain tool choice, state inspection, external verification, actions on systems, and side-effect sequencing. `AGENTS.md` remains the complete runtime profile; use this document for maintenance, audits, or explicit inspection, not task routing.

## Primary defaults

- Inspect current state before acting when state determines correctness.
- Choose the narrowest tool that accomplishes the goal.
- Treat destructive or hard-to-reverse actions as requiring clear intent, a recovery path, or confirmation.

## Do

- Classify each action as read-only, additive, modifying, or destructive.
- Prefer read -> plan -> write -> validate sequencing.
- Validate the result of each action before chaining the next.
- Reuse prior observations instead of re-querying when state has not changed.
- Use authoritative sources for current external facts and cite or mark uncertainty when needed.

## Avoid

- Running broad or recursive operations to answer narrow questions.
- Chaining destructive actions without intermediate checks.
- Using a powerful tool when a simpler one suffices.
- Acting on stale assumptions about system state.
- Exposing secrets, credentials, private keys, tokens, cookies, or unrelated personal data.

## Procedure

1. Identify the state or fact that controls correctness.
2. Choose the lightest available read or verification tool for that source of truth.
3. Inspect only the relevant target, config, output, page, source, or artifact.
4. Plan the smallest useful action.
5. Execute and capture the result.
6. Validate against the expected post-state.
7. For destructive or hard-to-reverse work, ensure the exact target and recovery path are clear before proceeding.

## Output pattern

- Source of truth inspected.
- Action taken or recommended.
- Observed result.
- Validation check and outcome.
- Pending confirmation only when low-risk progress is blocked.

## Stop when

- The goal state is reached and validated, or
- a required confirmation is pending, or
- an error blocks low-risk continuation.
