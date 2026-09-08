---
name: quick-proto
description: Track B low-fidelity prototyping for PMs, POs, BAs and other non-designers — fast, style-agnostic, grayscale flow prototypes that show an idea or compare multiple versions of a flow. Follows core UX best practices with hard constraints against visual polish. Use when someone needs to show how a flow works without needing it to look designed, or without codebase access.
---

# /quick-proto — Fast, Style-Agnostic Flow Prototyping

This skill exists to show **an idea, a flow, or multiple competing versions of a flow**, as
fast as possible. It is explicitly **not** about visual design or styling.

Built for PMs, POs, BAs and anyone else who needs to communicate a flow without design
tool proficiency and without codebase access. Output is intentionally illustrative, never
implementation-ready. For prototypes that use the real design system, use `/design-proto`.

## Hard constraints — non-negotiable

These are what keep the output fast, and honest about what it is:

- **Grayscale only.** Near-grayscale palette. Color is not part of what this skill
  communicates. The single exception is a functional signal that carries meaning (an
  error state) — and even then, keep it muted.
- **No decorative styling.** No rounded corners, no shadows, no gradients, no icons as
  decoration, no illustrations, no brand fonts, no hover flourishes, no animation. Nothing
  that could be mistaken for a real design direction.
- **Plain borders, plain type, generous whitespace.** One system font stack. Two or three
  sizes total. Boxes and rules — that's the entire visual vocabulary.
- **As simple as possible everywhere.** The question is "does this flow make sense," not
  "does this look good."

If the user asks to make it prettier, say plainly what this skill is for and offer the
real alternative: `/design-proto` if they have codebase access, or a designer if they
don't. Polishing a low-fi prototype defeats its purpose — people start reviewing the
styling instead of the flow.

## UX best practices — the floor, and nothing beyond it

Follow these; don't go further:

- **Clear hierarchy** — one obvious primary action per screen, secondary actions visibly
  subordinate.
- **Logical flow** — every screen shows where you came from and where you can go. No
  dead ends.
- **Obvious affordances** — buttons look like buttons, links like links, inputs like
  inputs. Labels above fields.
- **Real states** — empty, loading, error, and success states exist. A flow that only
  shows the happy path hasn't been prototyped.
- **Accessibility basics** — semantic HTML, labelled inputs, keyboard-operable controls,
  logical heading order, sufficient contrast even in grayscale.
- **Honest content hierarchy** — the most important thing on the screen is the most
  prominent thing on the screen.

## Copy rules

Copy should be minimal, purposeful, and realistic. **Explicitly avoid AI-slop copy** —
generic filler, over-explaining, walls of text, cheerful padding.

- If a screen needs a label, give it a short, real-sounding one. Don't pad it.
- No "Welcome to your dashboard! Here you can view all of your items in one convenient
  place." Just: "Saved items."
- Banned vocabulary: seamlessly, effortlessly, unlock, empower, elevate, supercharge,
  "your journey," "we're excited to."
- Realistic placeholder data, not `Item 1 / Item 2 / Item 3`. Fake data that looks like
  real data reveals real layout problems.

## Step 1 — Ask

Batched, with the usual escape hatch ("idk for now" / "take your best guess"):

1. **What flow?** Start point and end point.
2. **Who's walking through it,** and what are they trying to do?
3. **How many versions?** One flow, or competing approaches to compare?
4. **Any fixed steps** — required screens, legal/compliance gates, existing constraints?
5. **Where does it live** — mobile, desktop, both?

## Step 2 — Map before drawing

Write the flow out as a numbered step list and confirm it. Fixing a flow in a list takes
seconds; fixing it in screens takes an hour. Include branch points and failure paths.

## Step 3 — Build

Produce a single self-contained HTML file — screens laid out so the whole flow is visible
at once, with clickable navigation between them.

- **Screen title above each frame**, plus a one-line note on what happens here.
- **Flow order visible** — screens laid out left-to-right or top-to-bottom in sequence,
  with the connections between them legible.
- **Multiple versions side by side** when comparing. This is a primary use case, not an
  afterthought: label them Version A / Version B, keep them visually identical in
  treatment so only the structural difference stands out, and add a short note under each
  saying what bet it's making.
- **Interactive where it matters** — clicking the primary action moves to the next screen.
  Everything else can be inert.

Publish as an artifact so it can be shared and clicked through, unless the user wants a
local file.

## Step 4 — Hand over

Say what's shown, what's deliberately omitted, and what question the prototype is meant to
answer. Then offer the next step:

- Compare approaches with a persona → `/impersonate`
- Check it against usability heuristics → `/usability-audit`
- Turn the chosen version into engineering-ready detail → `/spec-redline`
- Build it for real in the design system → `/design-proto`

## Failure modes to avoid

- **Drifting into design.** The moment shadows and brand color appear, reviewers start
  reviewing the wrong thing.
- **Happy path only.** Empty, error, and edge states are usually where the flow is wrong.
- **Copy slop.** Padded, cheerful, generic copy makes a flow look fine when it isn't.
- **One version when they asked to compare.** Side-by-side comparison is the point.
- **Being mistaken for a spec.** Say out loud that this is illustrative, not
  implementation-ready — Track B always needs `/spec-redline` before engineering.
