# Evaluation Rubric

Use this rubric to test whether a summary is source-faithful across text, video transcripts, audio transcripts, interviews, and meetings.

## Scores

Score each dimension from 0 to 5.

- 5 — strong: faithful, specific, traceable, no meaningful omission.
- 4 — good: mostly faithful; minor omissions or light weight mismatch.
- 3 — acceptable: main idea survives, but some examples/limits/roles are weak.
- 2 — weak: source recognizability is low; major details missing.
- 1 — poor: frequent distortion or unsupported inference.
- 0 — fail: summary does not reflect the source.

## Dimensions

1. **Main-thread fidelity**
   - Does the summary preserve what the source is mainly doing?

2. **Attention-weight match**
   - Does the output emphasize what the source spends time on?

3. **Concrete evidence/examples**
   - Are key examples, named details, and evidence preserved?

4. **Action/argument chain**
   - Does it preserve the source's sequence of reasoning, action, or discussion?

5. **Decision-model fidelity**
   - Does it explain why major actions/claims follow from constraints, tradeoffs, or failure modes?

6. **Boundary and uncertainty handling**
   - Does it preserve caveats, undecided items, speaker roles, and source quality limits?

## Deductions

Apply deductions after the 30-point score:

- Major hallucination: -5
- Reversed conclusion: -5
- Speaker/author attribution error: -3
- Decision/action status error: -3
- Important caveat removed: -2
- External analysis mixed into source summary: -2

## Verdict

- **Pass**: 24+ after deductions, no major hallucination, no conclusion reversal.
- **Partial pass**: 18–23, or 24+ with non-fatal but important omissions.
- **Fail**: below 18, or any severe source distortion.

## Scenario-specific checks

### Text/article/report

- Are thesis, arguments, evidence, counterpoints, and caveats preserved?
- Are rhetorical flourishes kept subordinate to the main argument?

### Video transcript / lecture / demo

- Are timestamps or approximate source ranges included for key claims?
- Are demos and concrete steps preserved, not collapsed into slogans?

### Audio/podcast transcript

- Are speaker roles, recurring themes, stories, and disagreements preserved?
- Are host questions not confused with guest conclusions?

### Interview

- Is the Q&A relationship preserved?
- Are hesitations, uncertainty, and revised answers represented accurately?

### Meeting transcript

- Are decisions, action items, owners, deadlines, risks, blockers, and unresolved questions separated?
- Are suggestions not mislabeled as decisions?
