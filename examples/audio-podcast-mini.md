# Mini Example: Audio / Podcast Transcript

This fictional example shows how the skill handles speaker attribution and disagreement.

## Source excerpt

Host: Today we're asking whether small teams should adopt AI coding tools immediately.

Guest A: I think yes, but only for codebases with strong tests. Otherwise the model moves faster than your ability to verify it.

Guest B: I agree on tests, but I worry more about review overload. Our bottleneck was not writing code. It was understanding what changed.

Host: So is the blocker test coverage or review capacity?

Guest A: For us, test coverage came first. Once tests existed, reviews became smaller.

Guest B: In our case, even with tests, reviewers were overwhelmed because pull requests were too large.

## Weak generic summary

The guests agree that AI coding tools are useful for small teams if they have tests and review practices.

## Source-faithful summary

The discussion is not a simple consensus that small teams should adopt AI coding tools. Both guests support adoption only with constraints, but they identify different bottlenecks. Guest A says strong tests are the gating condition because otherwise AI changes outrun verification. Guest B agrees tests matter but says review capacity was the larger bottleneck: even tested changes became hard to understand when pull requests were too large. The host frames this as a choice between test coverage and review capacity; the guests' examples show that the limiting factor depends on the team's workflow.

## Attribution check

- Host: frames the question and clarifies the disagreement.
- Guest A: prioritizes test coverage.
- Guest B: prioritizes review capacity and PR size.
