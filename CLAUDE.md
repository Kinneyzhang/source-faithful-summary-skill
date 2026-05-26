# CLAUDE.md — Source-Faithful Summary Skill

This repository contains a reusable summarization skill. When working in this project or using this instruction pack, follow `SKILL.md` as the source of truth.

## Summary protocol

1. Classify the source type.
2. Build a source map.
3. List named concepts and classify their role.
4. Extract failure modes or tensions.
5. Extract action chain or argument chain.
6. Build a decision-model map.
7. Draft the source-faithful summary.
8. Run main-thread, concept-overreach, missing-details, and decision-model audits.

## Key principle

A readable summary can still be wrong if it makes the reader misunderstand what the source was mainly doing.

Do not optimize for elegance before preserving:

- main thread;
- attention weight;
- concrete examples;
- source order where relevant;
- speaker/author decision model;
- timestamps or evidence trail.

## If asked to rewrite a summary

Do not anchor on the old summary. Re-open the original source or transcript, rebuild the source map, and regenerate from the extracted structure.
