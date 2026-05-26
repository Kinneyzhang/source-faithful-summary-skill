# Source-Faithful Summary Skill

[English](README.md) | [简体中文](README.zh-CN.md)

An agent skill for source-faithful summaries of text, video transcripts, audio transcripts, podcasts, interviews, lectures, demos, workshops, and meetings.

Most AI summaries optimize for clean prose and abstract takeaways. That often produces a readable article that no longer reflects what the source actually spent time on. This skill optimizes for source fidelity: main thread, attention weight, concrete examples, action sequence, failure modes, evidence, and the speaker or author's decision model.

## Why this exists

Long-form summaries often fail in subtle ways:

- they replace the source's actual flow with the summarizer's cleaner framework;
- they mention concepts but miss why those concepts control later actions;
- they compress examples into slogans;
- they add implications before preserving what the source actually said;
- they pass factual checks but fail the “would a knowledgeable reader/viewer/listener recognize this?” test.

This package gives agents a repeatable method for source-grounded summarization.

## What it supports

- **Text**: articles, essays, reports, interview transcripts, meeting notes, lecture notes.
- **Video**: YouTube, Bilibili, conference talks, courses, workshops, demos — once a transcript is available.
- **Audio / voice**: podcasts, interviews, meeting recordings, voice notes, lectures — once transcribed.

This package does not do speech-to-text by itself. Use your own transcript tool first, then apply this skill.

## What it includes

- `SKILL.md` — canonical Hermes skill and full workflow.
- `AGENTS.md` — generic instructions for coding/agent CLIs such as Codex, OpenCode, Gemini-style agents, and other project-aware agents.
- `CLAUDE.md` — Claude Code adapter.
- `.cursor/rules/source-faithful-summary.mdc` — Cursor/Windsurf-style editor rule.
- `templates/source-map.md` — worksheet for source maps and decision-model extraction.
- `templates/summary-outline.md` — reusable outline for source-faithful summaries.
- `templates/evaluation-rubric.md` — scoring rubric for multi-scenario evaluation.
- `templates/long-source-plan.md` — worksheet for long transcripts, podcasts, panels, and long articles.
- `examples/workflow-talk-mini.md` — small workflow/video-style example.
- `examples/text-article-mini.md` — text article example.
- `examples/audio-podcast-mini.md` — multi-speaker audio/podcast transcript example.
- `examples/meeting-mini.md` — meeting transcript example.

## Core idea

```text
Faithfulness to the source > elegance of argument
Narrative weight > concept density
Concrete action/problem chain > abstract framework
Evidence > vibes
Speaker/author decision model > isolated tips
```

For practical/workflow material, use this extraction primitive:

```text
failure mode → underlying constraint → speaker/author judgment → concrete action → tradeoff/limit
```

## Quick start

Clone the repo:

```bash
git clone https://github.com/Kinneyzhang/source-faithful-summary-skill.git
cd source-faithful-summary-skill
```

Use the skill in any agent by reading `SKILL.md` before summarizing a source.

With Hermes Agent, copy or symlink the repo into your skills directory according to your setup, or use it as a project-backed skill.

Example symlink:

```bash
mkdir -p ~/.hermes/skills/research
ln -s "$(pwd)" ~/.hermes/skills/research/source-faithful-summary-skill
```

Then load it in a new Hermes session:

```bash
hermes -s source-faithful-summary-skill
```

## How to use

Before writing prose, make the agent produce these intermediate artifacts:

1. Source type classification.
2. Source map with timestamps or section references.
3. Named concepts and role classification.
4. Failure modes or tensions.
5. Action/argument chain.
6. Decision-model map.
7. Main-thread audit.
8. Reverse-summary audit.

Only then write the final summary.

## Minimal prompt

```text
Use the Source-Faithful Summary Skill.
First classify the source type, build a source map, list named concepts, extract failure modes/tensions, action or argument chain, and decision-model map.
Then write a summary that preserves the source's main thread and attention weight.
Do not turn the source into a polished concept essay.
```

## Good fit

Use this for:

- source-grounded summaries of articles, reports, and transcripts;
- YouTube/Bilibili/Vimeo talks after transcript extraction;
- podcasts and audio interviews after transcription;
- technical demos and workshops;
- lectures and conference talks;
- public articles that need to faithfully represent one source;
- auditing whether an existing summary missed the source.

## Not a good fit

Do not use this as the primary workflow for:

- free-form opinion essays inspired by a source;
- marketing copy;
- summaries where source fidelity is not important;
- broad research articles that intentionally synthesize many sources before preserving any one source.

## Long-source support

For sources longer than ~50k characters or ~60 minutes, use `templates/long-source-plan.md` before writing prose. It makes the agent state its chunking/sampling strategy, chapter coverage, recurrence checks, speaker coverage, and evidence budget. This is especially important for podcasts, panels, long workshops, and extracted webpages where figures or tables may be missing.

## Limitations

- The skill does not fetch transcripts or run STT by itself.
- Poor OCR, extraction, subtitles, or speech-to-text can distort details; mark that limitation when present.
- It prioritizes source fidelity over elegance. If you want analysis or implications, add them as a clearly separated second stage.

## License

MIT
