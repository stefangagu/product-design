---
name: research
description: Run product research the way a product researcher would — framed around product decisions, hypotheses and open questions rather than generic web summarization. Outputs insight → implication → recommendation with real, verifiable sources and explicit confidence labels. Use when the user asks to research a problem space, users, competitors, or a market question for a product decision.
---

# /research — Product-Oriented Research

Generic research answers "tell me about X." Product research answers "what should we do
about X, and how sure are we?" This skill only does the second kind.

## Non-negotiables

1. **Every claim carries a real, verifiable source.** A URL, a named report, a document,
   a dashboard, a transcript. Never fabricate a citation, never attribute vaguely
   ("studies show", "research suggests", "it's well known that"). If a claim cannot be
   sourced, mark it `[Unverified]` and present it as a hypothesis to test — not a finding.
2. **Every output carries confidence labels** — `[Grounded]`, `[Inferred — from X]`,
   `[Assumed — X would confirm]` — as a standard part of the format, not only when
   guessing. See `shared/interaction-principle.md`.
3. **Ask where the output goes** before finalizing. Never assume a destination.

## Step 1 — Frame the research around a decision

Before searching anything, establish what decision this research serves. Ask, in one
batched message, and make clear the user can say "idk for now" or "take your best guess":

1. **What decision does this inform?** (Build/don't build, which direction, how to
   prioritize, whether a hypothesis holds.)
2. **What's the hypothesis or open question?** State it as something that could be wrong.
3. **Who is the user segment** in scope?
4. **What's already known / already been tried?** Prior research, analytics, support
   themes, failed attempts.
5. **What constraints bound the answer?** Timeline, platform, regulatory, tech.
6. **What would change your mind?** The single finding that would flip the decision.

If the user opts out on any of these, proceed and label the gap explicitly in the output's
confidence summary. Do not silently pick a segment or invent a hypothesis.

Then restate the framing back in two or three lines and start. Do not wait for approval
unless the framing is genuinely ambiguous.

## Step 2 — Choose product-research methods, not generic search

Map the question to the practice that actually answers it:

| Question shape | Method to run |
| :-- | :-- |
| "What do users need here?" | Jobs-to-be-done framing — job, circumstance, current workaround, hiring criteria |
| "Why do users drop off?" | Funnel + friction analysis against the flow; support/review mining |
| "What are competitors doing?" | Structured competitive teardown — flow-by-flow, not feature checklists |
| "Is this interface any good?" | Heuristic evaluation (Nielsen's 10) against the actual flow |
| "Is there a market for this?" | Sizing + demand signals + willingness-to-pay evidence, each sourced |
| "What's the standard pattern?" | Convention survey across named products, with screenshots/links |

Prefer primary evidence in this order: the product's own data and user-facing artifacts >
named competitor products you can actually inspect > public research with a citable
source > general web summary (weakest — label `[Inferred]` at best).

**Competitive teardowns** are structured by flow, not by feature list: entry point →
each step → the decision the design is making → what it costs the user → what it implies
for us. A feature checklist is not a teardown.

## Step 3 — Output format

Never a loose report. Always this shape:

```markdown
# Research: <question, phrased as the decision it serves>

**Decision this informs.** <one line>
**Hypothesis.** <the thing that could be wrong>
**Method.** <what was actually done, honestly — including what wasn't>

## Findings

### <Short insight title>
**Insight.** <what is true> [Grounded — <source>]
**Implication.** <what it means for this product specifically — not a generic truism>
**Recommendation.** <concrete enough to act on this sprint>
**Confidence.** Grounded | Inferred | Assumed — <the one thing that would raise it>

<repeat per finding — 3 to 7 findings; more than that means it isn't synthesized yet>

## What we still don't know
<open questions, ranked by how much they'd change the decision>

## Sources
<numbered, real, clickable. Each finding references these by number.>

**Confidence summary**
- Grounded: <what came from the user or a real source>
- Inferred: <what was derived, and from what>
- Assumed: <what was guessed, and what would confirm it>
```

## Step 4 — Deliver

Before finalizing, ask where the output should go:

- **Markdown file** at a path they name — recommend `research/<question>.md`
- **Claude artifact** — a shareable, published page
- **Confluence / Google Drive / Notion** — only if such a connector is actually attached
- **Terminal only**

If the user opts out of choosing, write the markdown file at the recommended default and
say plainly where you put it.

## Failure modes to avoid

- **Assuming a destination.** Never decide on the user's behalf where output lands. Ask.
- **Insight inflation.** "Users want it to be easy" is not a finding. If it would be true
  of any product, cut it.
- **Recommendations that aren't actions.** "Consider improving discoverability" is a
  restatement. "Move saved-items into the tab bar and default the tab to Recent" is a
  recommendation.
- **Confidence laundering.** An inferred claim written in the register of a grounded one.
  If it's a guess, label it a guess.
- **Padding with method description.** Report what was found, not how hard you looked.
