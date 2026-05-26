# Source-Faithful Summary Outline

## One-sentence faithful summary

<One sentence that preserves the source's actual main thread.>

## Source type and spine

- Source type:
- Summary spine:

## 1. What the source is reacting to

<Problem, default assumption, failed workflow, debate context, or opening tension.>

## 2. The first major claim or action

<Concrete claim/action with evidence.>

## 3. The constraint or mental model behind it

<Why this claim/action is necessary.>

## 4. The source's action/argument chain

<Preserve order and weight.>

## 5. Concrete examples

<Examples that carry the source, not generic paraphrases.>

## 6. Limits, tradeoffs, and boundaries

<What the speaker/author warns about or does not claim.>

## 7. Decision model map

- Constraint:
  - Failure:
  - Judgment:
  - Action:
  - Tradeoff:
  - Evidence:

## 8. Practical checklist / takeaway

<Only if the source supports it.>

## 9. Source notes

- <timestamp or section>: <fact>


---

# Reader-Facing Article Mode

Use this when the output should be a publishable/readable summary, not an audit artifact.

## Title

`# <Source / speaker>: <actual workflow/problem the source explains>`

The title should be source-specific. Avoid generic titles like “why fundamentals matter” when the source actually demonstrates a workflow.

## Opening block

- Source:
- Transcript/source quality:
- Source type:
- Main spine:
- One-sentence faithful summary:

## Numbered body

Use 8–14 source-specific sections for long workflow material. Each heading should name one constraint, artifact, action, feedback loop, or caveat from the source.

Good section headings:

- `约束一：smart zone / dumb zone —— 任务必须切到模型能聪明处理的范围内`
- `第一段动作：用 Grill Me 把模糊需求变成共享理解`
- `Review 要用 fresh context：不要让 dumb zone 里的 agent 自审`

Weak section headings:

- `The problem`
- `The workflow`
- `Key takeaways`

## End matter

- Decision model map
- Copyable workflow checklist
- Do-not-misread section
- Timestamp source notes
- Final conclusion

## Rule

Working artifacts such as source maps, long-source plans, and scoring rubrics belong in an appendix/evaluation report unless the user asks to inspect the process. They should not block the reader from the actual article.


## Revision / merge mode

Use when improving an existing good reader-facing article with additional facts from a newer run.

1. Identify the older article's strongest assets: title, opening spine, section rhythm, final conclusion.
2. Identify new facts from the newer run: missing concepts, late-source details, caveats, examples.
3. For each new fact, choose one placement:
   - new section;
   - merged paragraph in an existing section;
   - renamed existing heading;
   - checklist item;
   - source note only.
4. Do not append new facts mechanically. Preserve narrative rhythm.
5. If version A reads better and version B is more complete, use A as the narrative spine and absorb B's facts selectively.

## Strong workflow article pattern

For practical/workflow sources, a strong reader-facing article usually follows:

```text
Source type + spine + one-sentence summary
→ constraints / failure modes
→ first concrete action
→ external artifact/process
→ feedback/review loop
→ architecture/boundary
→ scaling/parallelization
→ decision model/checklist/do-not-misread/source notes
→ final conclusion
```
