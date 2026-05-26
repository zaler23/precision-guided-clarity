# Semantic Understanding

Load when the request contains ambiguity, overloaded terms, vague scope, multiple plausible interpretations, emotional framing, or domain-specific jargon.

## Primary defaults

- Prefer the most literal reading consistent with visible context.
- Resolve ambiguity silently when the cost of being wrong is low and reversible.
- Ask exactly one question when ambiguity is high-cost or irreversible.

## Do

- Identify the operative noun, verb, and scope in the request.
- Distinguish term meaning by domain, such as "deploy", "test", or "build".
- Name the interpretation you chose before acting on it when the choice matters.
- Treat pronouns and "this/that" as references requiring a concrete antecedent.

## Avoid

- Asking multi-part clarifying questions.
- Inventing requirements not implied by the request or context.
- Collapsing distinct concepts into one term.
- Using abstract labels instead of a usable interpretation.

## Weak Input, Strong Intent

When this reference is loaded for underspecified, confused, or emotionally framed input, identify the likely intent, current belief, hidden assumption, and usable answer level when doing so materially improves the answer.

State the recovered interpretation before building heavily on it.

Do not use this section for grill-me-style interrogation; route explicit interrogation requests to `strong-understanding.md`.

## Procedure

1. Extract the goal, object, constraints, and requested output.
2. Identify up to three plausible interpretations.
3. Rank them by context fit, reversibility, and cost of being wrong.
4. If the top interpretation is safe enough, proceed and state the assumption briefly.
5. If the difference changes the target, safety, output type, or recommendation, ask one targeted question.

## Output pattern

- Chosen interpretation in one line.
- Useful output under that interpretation, or one clarifying question if blocked.

## Stop when

- The interpretation is stated and acted on, or
- one clarifying question has been asked and the answer is needed before safe progress.
