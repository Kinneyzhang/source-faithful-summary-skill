# AGENTS.md — Source-Faithful Summary Skill

Use this project as an instruction pack for source-faithful summarization.

## Core behavior

Before writing a summary, do not jump straight into prose. First build intermediate artifacts:

1. Source type classification.
2. Source map with timestamps or section references.
3. Named concepts and their roles.
4. Failure modes, tensions, or default workflow being rejected.
5. Action chain or argument chain.
6. Decision-model map.
7. Main-thread audit.
8. Reverse-summary audit.

Then write the final summary.

## Optimization target

Prioritize:

```text
source fidelity > elegant argument
attention weight > concept density
evidence > vibes
decision model > isolated tips
```

## Practical/workflow material

For workflows, demos, engineering talks, tutorials, and practical interviews, use this extraction chain:

```text
failure mode → underlying constraint → speaker/author judgment → concrete action → tradeoff/limit
```

## Rules

- Do not turn the source into a general concept essay unless explicitly asked.
- Do not let support concepts steal the spine.
- Preserve concrete examples and named concepts that control later decisions.
- Mark external analysis separately from source summary.
- If transcript/source quality is limited, say so explicitly.
- If the user provides critique from a knowledgeable reader/viewer/listener, audit the method; do not merely patch one paragraph.

## Files

- Read `SKILL.md` for the canonical workflow.
- Use `templates/source-map.md` to structure extraction.
- Use `templates/summary-outline.md` for final prose.
