# Mini Example: Workflow Talk

This is a fictional example showing the difference between a generic summary and a source-faithful summary.

## Source excerpt

A speaker describes how their team used to ask an AI assistant to implement large features from long specs. The first version often looked impressive, but later changes became harder to review. The speaker noticed that the assistant made worse decisions as the chat grew longer. They changed the workflow: first ask the assistant to interview the product owner, then write a short requirements note, split work into small vertical slices, run tests after each slice, and review in a fresh context.

## Bad generic summary

The talk argues that AI development requires good software engineering fundamentals, including planning, testing, and code review.

## Better source-faithful summary

The speaker is not merely saying that software engineering fundamentals matter. They describe a specific failure mode: large specs sent into long AI chats produced impressive first drafts but increasingly hard-to-review code. Their diagnosis is that long sessions degrade the assistant's decision quality. Their workflow response is to keep tasks small and externalize state: interview the product owner, write a short requirements note, split the plan into vertical slices, run feedback loops after each slice, and use a fresh context for review.

## Decision model map

- Constraint: long AI sessions degrade decision quality.
  - Failure it causes: later implementation and review become unreliable.
  - Judgment: do not let large features live inside one growing chat.
  - Action: externalize requirements, split vertical slices, test each slice, review from a fresh context.
  - Tradeoff: more planning overhead, but better controllability.
