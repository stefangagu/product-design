---
name: research-synthesis
description: Turn raw research artifacts — interview transcripts, session notes, survey exports, support tickets, app reviews, analytics dumps — into structured themes, evidence-backed insights, and persona updates. Use when the user has existing raw research material that needs to be analyzed rather than new research that needs to be conducted.
---

# /research-synthesis — Raw Artifacts → Structured Insight

The distinction from `/research`: that skill *conducts* investigation, this one *analyzes
material that already exists*. If the user has transcripts, exports, or ticket dumps, this
is the skill.

## Step 1 — Intake

Ask, in one batched message (user may say "idk for now" / "take your best guess"):

1. **Where is the material?** File paths, a folder, pasted text, a Drive/Confluence link.
2. **What kind, and how much?** N interviews, N survey responses, date range.
3. **Who did it cover?** Segment, recruiting criteria — this bounds what the findings
   can legitimately claim.
4. **What question was it collected to answer?** If it was collected for a different
   question than the one being asked now, say so — that's a real limitation.
5. **Any prior themes** to reconcile against, or is this a cold pass?

Read every artifact fully before coding anything. Partial reads produce confident nonsense.

## Step 2 — Code, then cluster

Work bottom-up. Do not start from a theory and find quotes for it.

1. **Extract observations.** Concrete, atomic, quoted where possible. One observation per
   line, each tagged with its source (`P4`, `ticket-1893`, `review-2026-03-11`).
2. **Cluster observations into themes.** A theme needs **at least three independent
   sources** to be called a theme. Two is a signal. One is an anecdote — keep it, label
   it, never promote it.
3. **Count honestly.** "6 of 12 participants" beats "many users." Report denominators
   always. If the sample is 8 people, no finding gets to say "users generally."
4. **Look for the disconfirming case.** Every theme gets checked against evidence that
   contradicts it. If none exists in the data, say the data didn't test it.

## Step 3 — Output

```markdown
# Synthesis: <corpus name>

**Corpus.** <N artifacts, type, date range, who they cover>
**Question this was collected to answer.** <original> — <note if it differs from current use>
**Limitations.** <sample size, recruiting bias, recency, what this data cannot tell us>

## Themes

### T1. <Theme name — stated as a finding, not a topic>
**What we saw.** <the pattern> — **<n> of <N> sources** (P2, P4, P7, ticket-1893)
**Representative evidence.**
> "<verbatim quote>" — P4
> "<verbatim quote>" — P7
**Counter-evidence.** <contradicting cases, or "none present in this corpus">
**Implication.** <what it means for the product>
**Confidence.** Grounded | Inferred | Assumed — <what would raise it>

## Outliers worth keeping
<single-source observations that are interesting but not themes — explicitly labelled>

## Persona updates
<what these findings change about existing personas — traits to add, revise, or retire.
Frame as diffs against the current persona document, not a rewrite.>

## Recommended next research
<the questions this corpus raised but cannot answer>
```

Theme names must be findings. "Onboarding" is a topic. "Users abandon onboarding at the
permissions screen because the value exchange hasn't been established yet" is a theme.

## Delivery

Before finalizing, ask where the output should go — a short menu, not a blocking gate:

- **Markdown file** at a path they name — recommend `research/synthesis-<corpus>.md`
- **Claude artifact** — a shareable, published page
- **Split per theme** into separate documents, if the themes will be worked on independently
- **Confluence / Google Drive / Notion** — only if such a connector is actually attached
- **Terminal only**

If the user opts out of choosing, write the markdown file at the recommended default and
say plainly where you put it.

## Handoff

- Persona updates feed `/persona` — offer to run it to apply them.
- Findings that need new investigation feed `/research`.
- Flow problems that need testing feed `/impersonate` or `/usability-audit`.

## Failure modes to avoid

- **Assuming a destination.** Never decide on the user's behalf where output lands. Ask.
- **Quote mining.** Picking quotes that fit a conclusion reached before reading.
- **Theme inflation.** Twelve themes from eight interviews means nothing was synthesized.
  Aim for three to six.
- **Losing the denominator.** "Users said" with no count is unusable.
- **Silent smoothing.** Contradictions in the data are findings, not noise to average out.
