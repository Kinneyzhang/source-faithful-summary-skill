---
name: source-faithful-summary-skill
description: Use when summarizing text, video transcripts, audio transcripts, podcasts, lectures, interviews, demos, or meetings where the output must preserve the source's main thread, attention weight, decision model, concrete examples, and evidence instead of becoming a polished but source-drifting essay.
version: 1.0.0
author: Kinney Zhang
license: MIT
metadata:
  hermes:
    tags: [video, transcript, summary, source-grounded, faithful-summary, ai-agents]
    related_skills: []
---

# Source-Faithful Summary Skill

## Overview

Use this skill for source-grounded summaries of text, video transcripts, audio transcripts, podcasts, talks, interviews, demos, workshops, lectures, meetings, and other transcript-like source material.

The goal is not to write the most elegant essay. The goal is to preserve what the source actually does: the speaker's main thread, attention weight, concrete examples, sequence, failure modes, actions, and decision model.

A summary can be factually plausible and beautifully written while still being wrong for the task if it replaces the speaker's actual flow with the summarizer's cleaner framework.

Core rule:

```text
Faithfulness to the source > elegance of argument
Narrative weight > concept density
Concrete action/problem chain > abstract framework
Timestamps/evidence > vibes
Speaker's decision model > isolated tips
```

## What This Skill Optimizes

A good source-grounded summary is not merely compressed source text. It should recreate the understanding a careful reader, viewer, or listener would get after engaging with the source.

Optimize for five kinds of fidelity:

1. **Main-thread fidelity** — what the speaker is actually driving toward.
2. **Attention fidelity** — what the speaker spends time on, repeats, or uses to explain later actions.
3. **Causal fidelity** — why one observation leads to the next decision.
4. **Action fidelity** — what the speaker actually does, in usable sequence.
5. **Decision-model fidelity** — the constraints, tradeoffs, and failure modes behind the speaker's workflow.

For workflow/practice sources, named concepts must not be treated as decorative keywords. A concept is important if it controls later decisions.

Example:

```text
smart zone / dumb zone
```

In an AI coding workflow talk, this is not just a definition about context degradation. It may explain why tasks are sized small, why context is cleared, why external artifacts like PRDs/Kanban boards matter, and why review should happen in a fresh context.

Default extraction primitive:

```text
failure mode → underlying constraint → speaker's judgment → concrete action → tradeoff/limit
```

## When to Use

Use when the user asks to:

- summarize a YouTube, Bilibili, Vimeo, podcast, interview, lecture, demo, workshop, or recorded meeting;
- rewrite or publish a source-based summary;
- audit whether an existing summary missed the original material's key points;
- extract a speaker's workflow, examples, failure modes, or practical advice;
- turn a long transcript into a public article or private note;
- compare a summary against a source transcript;
- preserve what the source says before writing independent commentary.

Also use when the source is not literally video but has a strong original sequence, such as an interview article, lecture notes, meeting transcript, or conference talk transcript.

Do **not** use this as the primary workflow when the user explicitly wants:

- a free-form opinion essay inspired by a source;
- a broad research article that uses the material as one source among many;
- creative rewriting that intentionally departs from the source;
- marketing copy where source fidelity is not required.

If commentary is needed, first produce the source-faithful summary, then add a clearly separated section such as “Analysis”, “Implications”, or “What this means for us”.

## Required Inputs

Prefer one or more of:

- transcript with timestamps;
- source URL plus transcript tool access;
- existing summary to audit;
- target audience and output length;
- whether the result is public-facing or private notes;
- desired language.

If the transcript is unavailable, state the limitation explicitly and summarize only from available material.

## Standard Workflow

### Step 1 — Fetch and validate source material

Get transcript or source text before summarizing.

Validation checklist:

- source text is non-empty;
- language is known;
- duration/segment count looks plausible if video/audio;
- timestamps are preserved when available;
- missing transcript or poor subtitle quality is noted.

If transcript fetch fails, retry with another language or source when possible. Do not hallucinate details from the title alone.

### Step 2 — Classify the source type

Do not write the summary yet. First classify the material:

```text
1. Viewpoint talk: core is a thesis and supporting arguments.
2. Practical/workflow talk: core is a sequence of problems and actions.
3. Tutorial/demo: core is steps, commands, screens, and gotchas.
4. Interview: core is the guest's experiences, claims, and examples.
5. Product/update talk: core is features, changes, migration impact.
6. Research/lecture: core is definitions, evidence, method, conclusion.
7. Debate/panel: core is positions, disagreements, and evidence.
```

Write one line before drafting:

```text
Source type: <type>; primary summary spine should be <argument chain / action chain / step chain / Q&A chain / feature-impact chain / disagreement map>.
```

If the material is practical/workflow, the default spine must be:

```text
problem → failure mode → speaker's action → tool/prompt/process → result/lesson
```

### Step 3 — Build a source map

Create a source map before prose. It should include:

```text
- Timestamp range or source section
- What happens in this segment
- Speaker's concrete example or claim
- Role: main thread / support concept / example / aside / implication
- Why it matters
```

Minimum shape:

```markdown
## Source map

- 00:00–01:10 — Setup: speaker frames the problem. [main]
- 01:10–03:40 — Failure mode: what breaks in the default workflow. [main]
- 03:40–05:15 — Concept used to explain the failure. [support]
```

Do not collapse practical details into abstract concepts during this step.

### Step 4 — Extract named concepts and source roles

List speaker-coined, repeated, or emphasized terms.

For each term, classify it:

- **Controlling concept:** explains several later actions or decisions.
- **Support concept:** helps explain the main thread but is not the spine.
- **Example label:** names one concrete case.
- **Aside:** interesting but not central.

Rules:

- A controlling concept must appear in the summary.
- Support concepts cannot become the headline or spine unless the source itself is a concept lecture.
- If a named concept explains multiple actions, write the action chain it controls.

### Step 5 — Extract the concrete chain

For practical/workflow material, answer:

```text
1. What did the speaker try first?
2. What failed?
3. What symptoms did they observe?
4. What constraint or mental model explains the failure?
5. What judgment did the speaker make because of that constraint?
6. What did they change?
7. What tool/skill/prompt/file/process did they use?
8. What improved?
9. What tradeoff, cost, or remaining limitation did they mention?
```

For AI/software workflow videos, also ask:

```text
- What AI-specific failure modes were named?
- What behaviors of models/agents were observed?
- What context/window/memory limits shaped the workflow?
- What feedback loops were recommended?
- What guardrails were proposed?
- Which parts are safe to delegate, and which require human review?
- Which named concepts control later actions rather than merely illustrate them?
```

### Step 6 — Extract the speaker's decision model

Before drafting, write a compact decision-model map:

```markdown
## Decision model map

- Constraint: <context degradation / forgetting / review overload / missing feedback>
  - Failure it causes: <what goes wrong>
  - Speaker's judgment: <what the speaker decides because of it>
  - Workflow action: <what they do in practice>
  - Evidence: <timestamp/source section>
```

If this map is missing, the summary will usually become a list of tips instead of a faithful account of the speaker's thinking.

### Step 7 — Draft a source-grounded outline

Choose outline by source type.

For practical/workflow videos:

```markdown
# <Speaker/topic>: <actual workflow or problem>

## One-sentence faithful summary
## 1. The problem the speaker was reacting to
## 2. The first failure mode they observed
## 3. The constraint or mental model behind the fix
## 4. The workflow/tool/process they introduced
## 5. The concrete checklist readers/viewers/listeners can copy
## 6. Limits, warnings, and where judgment remains necessary
## Source notes / timestamped facts
```

For viewpoint talks:

```markdown
## One-sentence thesis
## 1. What the speaker argues against
## 2. The speaker's main claim
## 3. Supporting arguments in source order
## 4. Examples and evidence
## 5. What the speaker does and does not claim
## Timestamped facts
```

For tutorials/demos:

```markdown
## What this teaches
## Prerequisites/context
## Step-by-step flow
## Gotchas and failure modes
## Final result
## Timestamped command/action notes
```

For interviews:

```markdown
## Who is speaking and why it matters
## Main claim or experience arc
## Key stories in source order
## Repeated themes
## Concrete examples
## What is claimed vs inferred
```

### Step 8 — Write the summary

Writing constraints:

- Preserve the source's main sequence unless there is a strong reason not to.
- Prefer concrete verbs: tried, observed, changed, scanned, generated, tested, reviewed.
- Include timestamps for key claims when useful.
- Do not add facts not in the source unless clearly marked as external context.
- Do not turn examples into generic principles too early.
- Do not let books/frameworks/concepts steal the main role from the speaker's actual actions.
- If translating, preserve tool names, command names, repository names, and technical terms accurately.
- Keep personal implications separate from source summary.

Good phrasing:

```text
The speaker first describes a concrete failure: they tried X, observed Y, and changed Z because constraint C made the original approach unreliable.
```

Risky phrasing:

```text
The core of the talk is that timeless engineering principles matter.
```

The second sentence may be true, but it likely over-abstracts a practical talk.

### Step 9 — Run audits before publishing

#### A. Main-thread audit

Ask:

```text
If a reader only reads this summary, what would they think the source is mainly about?
Does that match the transcript's actual main thread and time allocation?
```

If not, rewrite.

#### B. Missing-practical-details audit

For practical/workflow videos, check whether the summary includes:

- initial failed/default workflow;
- observed symptoms;
- concrete tools/prompts/skills/files;
- implementation steps;
- feedback loops;
- limitations and warnings;
- human review boundaries.

#### C. Concept-overreach audit

Check:

- Did a support concept become the headline or spine?
- Did the summary replace speaker actions with general principles?
- Did we add our own framework without marking it?
- Did implications crowd out source content?

#### D. Decision-model audit

For each major workflow action in the summary, verify:

```text
Do we explain why the speaker does this, not only that they do it?
Which constraint or failure mode makes this action necessary?
Would a reader be able to copy the speaker's judgment, not just the surface step?
```

Challenge prompts:

- Which speaker-coined or repeatedly used term is absent?
- Which concept explains several later actions but was treated as a minor definition?
- Which failure mode was omitted, causing the recommendation to look arbitrary?
- Which human-vs-agent boundary is unclear?
- If someone followed this summary, where would they misuse the workflow?

## Output Templates

### Short summary

```markdown
Core conclusion: <one sentence faithful to the source>

Source spine:
1. <problem/failure mode>
2. <speaker action/workflow>
3. <result/lesson>

Easy-to-miss details:
- <detail with timestamp>
- <detail>
```

### Public article

```markdown
# <Speaker/topic>: <actual workflow or problem>

Source:
- <URL or source name>
- Transcript: <language/count/duration, if available>

## One-sentence faithful summary

<Do not over-abstract.>

## 1. <First source segment / problem>
## 2. <Speaker's first concrete move>
## 3. <Next failure mode or workflow step>
## 4. <Practical checklist>
## Decision model map
## Timestamped facts
```

### Audit report

```markdown
## Verdict

- Faithfulness: pass/fail
- Main-thread match: pass/fail
- Missing practical details: <list>
- Concept overreach: <list>
- Decision-model fidelity: <pass/fail>

## Evidence

- 01:12–02:14: <transcript-backed point>
- 06:38–07:15: <transcript-backed point>
```

## Common Pitfalls

1. **Writing a better essay than the source summary.** Good prose is not enough. If the main thread changed, it failed.

2. **Letting support concepts steal the spine.** A speaker may cite famous frameworks to explain practice. Unless the talk is about those frameworks, they are support, not the main story.

3. **Ignoring time allocation.** If the source spends five minutes on workflow failures and thirty seconds on a concept name, reflect that weight.

4. **Compressing examples into slogans.** Keep concrete examples, especially for practical takeaways.

5. **Mixing implications into source summary.** Public readers usually need the source first. Put analysis in a separate section.

6. **Only auditing facts, not task fit.** A summary can have no factual errors and still answer the wrong question.

7. **No reverse-summary check.** Always ask what a reader would think the original was about after reading your summary.

8. **No timestamp trail.** Key claims should be traceable to source ranges, even if the final prose does not cite every line.

9. **Responding to critique with paragraph patches.** Critique from a knowledgeable reader, viewer, or listener often means the summary method missed the source's decision model. Audit the method before patching prose.

## Verification Checklist

Before finalizing:

- [ ] Source/transcript fetched or limitation stated.
- [ ] Source type classified.
- [ ] Source map exists.
- [ ] Named concepts are listed and role-classified.
- [ ] Main thread is stated in one sentence.
- [ ] Practical/workflow material includes the concrete action/failure chain.
- [ ] Decision-model map exists for major actions.
- [ ] Support concepts are not the main spine unless source type justifies it.
- [ ] Public/private implications are separated.
- [ ] Missing-practical-details audit passed.
- [ ] Decision-model audit passed.
- [ ] Reverse summary matches source main thread.
- [ ] If published, the final page or file was fetched back and checked.
