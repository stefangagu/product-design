---
name: handoff-pr
description: Track A dev handoff — packages an in-repo prototype built with /design-proto into a PR-ready review package with a summary of changes, affected components, what's real vs. stubbed, and open questions for engineering. Turns handoff into a code review cycle rather than a spec-writing exercise. Use after building an in-repo prototype that engineering needs to pick up.
---

# /handoff-pr — Track A: PR-Ready Handoff

When the prototype was built in the real codebase with the real design system, handoff
becomes **near-zero-translation**: closer to "here's a branch, review and refine" than
"here's a spec, please build this." The code *is* the spec. There is no design-vs-code
interpretation gap, because there is no separate design artifact to interpret.

This skill packages that branch so engineering can pick it up in a normal code review
cycle instead of a redline cycle.

Requires an in-repo prototype (`/design-proto`). For low-fi Track B prototypes, use
`/spec-redline` — those genuinely still need a full spec.

## Step 1 — Establish what shipped

Read the actual diff. Don't ask the user to summarize their own work — derive it, then
confirm.

1. `git diff` against the base branch — every file, not just the summary stat
2. Which existing components were used, and how
3. Whether anything new was created, and whether permission was given for it
4. What's real, what's stubbed, what's faked
5. Which states exist and which don't

Then ask, briefly, only what the diff can't tell you:

1. **What question was this prototype answering?** The design intent.
2. **What's still open** — decisions deliberately deferred?
3. **What's deliberately fake** that a reviewer might read as real?
4. **Any known trade-offs** taken to get it working?

## Step 2 — The critical guardrail

State prominently, at the top of the handoff, that **prototype code is not production
code**. This is the single biggest risk of Track A: work that looks shippable because it
sits in the real codebase and uses the real components.

Be specific about what's missing rather than issuing a generic disclaimer. Go through the
diff and name it: stubbed data sources, absent error handling, missing loading states,
unhandled edge cases, no tests, no analytics, no telemetry, unconsidered performance,
security not reviewed, i18n not applied, accessibility only at the design-system floor.

The design needs no translation. The engineering still does. Say that plainly.

## Step 3 — Write the handoff package

```markdown
# Handoff: <feature name>

**Branch.** `<branch>` · **Base.** `<base>` · **Built with.** /design-proto
**Design question this answers.** <what it was exploring>

> ⚠️ **Prototype, not production.** This is design-accurate and engineering-incomplete.
> Specifically missing: <the real list, derived from the diff>.

## What's here
<2–4 sentences: what a reviewer will see when they run it, and the route to visit>

## Screens and states
| Screen | Route | States built | States not built |
| :-- | :-- | :-- | :-- |

## Components used
| Component | Source | Used for | Modified? |
| :-- | :-- | :-- | :-- |
<Every existing design-system component the prototype consumes.>

## New components created
<If any: what, why an existing component didn't fit, whether permission was given, and
whether this should be promoted into the design system or refactored away. If none —
say "None" plainly. That's the good outcome and worth stating.>

## Design decisions worth knowing
<decisions embedded in the code that a reviewer would otherwise have to reverse-engineer,
each with its rationale — this is the part that would have been a spec>

## Real vs. stubbed
| Area | Status | Notes |
| :-- | :-- | :-- |
| Saved items list | Stubbed — hardcoded fixture in `fixtures/saved.ts` | Needs the real endpoint |

## Open questions for engineering
<numbered, each with why it matters and who needs to answer it>

## What I'd expect to change in review
<where the prototype knowingly cut corners that engineering should redo properly>

## How to run it
<exact commands and route>
```

## Step 4 — Deliver

Ask where the handoff package should go:

- **A PR description** — recommended, since the package is written for reviewers and this
  puts it where the review happens
- **Markdown file** at a path they name — recommend `docs/handoff/<feature>.md`
- **Claude artifact** — a shareable page for stakeholders outside the repo
- **Confluence / Google Drive / Notion / a ticket** — only if such a connector is attached
- **Terminal only**

If the user opts out of choosing, write the markdown file at the recommended default and
say where you put it — do **not** silently open a PR as the fallback.

If they choose the PR: ask before pushing or opening anything. Publishing to a shared repo
is an outward-facing action, and approval to write the document is not approval to push it.

Recommend labelling the PR clearly as a prototype (a `prototype` label, or a `[Prototype]`
title prefix) so it can't be merged by reflex.

## Handoff to review

Point the reviewer at `/drift-check` for later: once the production implementation lands,
that skill compares it back against this prototype and catches drift introduced after
handoff.

## Failure modes to avoid

- **Assuming a destination.** Never decide on the user's behalf where output lands. Ask.
- **A generic disclaimer instead of a specific list.** "May need refinement" tells a
  reviewer nothing. Name the stubs.
- **Summarizing without reading the diff.** The value here is precision.
- **Hiding new components.** If the prototype expanded the design system, that's the most
  important line in the document.
- **Writing a spec anyway.** If you're describing what the code should do, you've missed
  the point — the code does it. Describe intent, constraints, and gaps.
- **Pushing without asking.**
