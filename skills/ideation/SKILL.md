---
name: ideation
description: Rapid divergent concept generation from a brief or problem statement, plus A/B variant generation for copy and layout. Outputs multiple genuinely different structured directions, each with rationale — in text and description form, not built screens. Use when the user wants options, directions, alternatives, or copy/layout variants to compare.
---

# /ideation — Concept Directions & A/B Variants

Two modes in one skill:

- **Direction mode** — a problem statement in, a menu of divergent concept directions out.
- **Variant mode** — a specific element in, comparable copy and layout options out.

Both produce **text and descriptions, not screens**. The moment an option becomes
something someone can click through, it has crossed into prototyping — hand off to
`/quick-proto` (low-fi) or `/design-proto` (in-repo, high-fidelity).

## Step 1 — Ask before generating

Ideas generated without constraints are generic. Ask, in one batch, making clear the user
can say "idk for now" or "take your best guess":

1. **Target user** — which segment, or which persona document if one exists
2. **The problem** — stated as a user problem, not a feature request
3. **Business goal** — what success looks like for the company, and how it's measured
4. **Constraints** — platform, tech, timeline, regulatory, existing design system
5. **Tone / brand** — how this product is allowed to sound and behave
6. **Out of bounds** — what's already been rejected, and why

If the user opts out, generate anyway and label each direction with the assumption it
rests on. State assumptions up front, before the options, so the user can correct the
frame rather than re-reading five ideas built on a wrong premise.

## Direction mode

Generate **five to seven** directions. Fewer than five isn't divergence; more than seven
is padding.

Directions must be **genuinely different bets, not the same idea reworded**. Force spread
by varying the underlying axis:

- Who does the work — user organizes vs. system organizes
- When it happens — on demand vs. proactive vs. scheduled
- Where it lives — dedicated surface vs. embedded in an existing flow
- What it optimizes — speed vs. control vs. discovery vs. social
- How much it changes — incremental vs. structural rethink

Include at least one direction that is uncomfortable — that removes something, inverts an
assumption, or bets against the obvious answer. The safe five are usually all the same
idea.

```markdown
## Directions for: <problem statement>

**Assumptions this rests on.** <anything the user opted out of specifying>

### 1. <Direction name>
<One or two sentences of what it is.>
**Rationale.** <the bet it's making about users or the market>
**Strongest when.** <the condition that makes this the right answer>
**Breaks if.** <the condition that kills it>

<repeat>

## How these differ
<name the axes they vary along, so the user can choose a bet rather than a favourite>

## What I'd probe first
<the cheapest test that would separate the strongest two or three>
```

Every direction ends with a real "breaks if." A direction with no failure condition
hasn't been thought through.

## Variant mode

For copy: generate three to five variants that differ in **strategy**, not wording —
value-led vs. instruction-led vs. outcome-led vs. minimal. Name the strategy for each.

For layout: describe structure, not visuals — what's on the screen, in what hierarchy,
what the user is meant to do first. No styling language.

```markdown
## Variants: <element, e.g. "empty state on the saved items screen">

### Copy
- **A — <strategy>.** "<copy>"  *<why this works / what it assumes>*
- **B — <strategy>.** "<copy>"  *<...>*
- **C — <strategy>.** "<copy>"  *<...>*

### Layout (described, not built)
- **A.** <structure — e.g. centered icon, single line, primary CTA>  *<the bet>*
- **B.** <structure>  *<the bet>*
- **C.** <structure>  *<the bet>*

## What each pairing optimizes for
<so the user can pick a combination deliberately>

## How to tell which won
<the metric or signal that would actually settle it>
```

Copy must be short, real-sounding, and free of AI filler. No "seamlessly," no
"effortlessly," no "unlock the power of." If a real product wouldn't ship that sentence,
it isn't a variant.

## Delivery

Before finalizing, ask where the output should go — a short menu, not a blocking gate:

- **Markdown file** at a path they name — recommend `ideation/<problem>-directions.md`
- **Claude artifact** — a shareable, published page
- **One document per direction**, if they're going to be pitched or explored separately
- **Confluence / Google Drive / Notion** — only if such a connector is actually attached
- **Terminal only**

If the user opts out of choosing, write the markdown file at the recommended default and
say plainly where you put it.

## Handoff

- Chosen direction → `/quick-proto` to make it clickable, or `/design-proto` to build it
  in the real design system.
- Want a reaction before committing → `/impersonate` with a relevant persona.
- Direction rests on an unvalidated assumption → `/research`.

## Failure modes to avoid

- **Assuming a destination.** Never decide on the user's behalf where output lands. Ask.
- **Five flavours of one idea.** Check the axes. If all options answer the same question,
  regenerate.
- **The rationale that restates the idea.** "Rationale: this makes saved items easier to
  find" is not a rationale. The bet is: *users know what they saved but can't recall where
  they put it* — that's falsifiable.
- **Building instead of describing.** No code, no screens, no components in this skill.
- **Ranking too early.** Present the spread. Recommend at the end, in one line, and say
  what would change the recommendation.
