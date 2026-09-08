---
name: usability-audit
description: Automated usability issue flagging on a prototype, flow, or shipped screen — heuristic evaluation, accessibility checks (contrast, alt text, labels, focus and tab order), and flow-level issue detection. Returns a structured issue list with severity, the heuristic violated, and a concrete suggested fix. Use when a prototype or screen needs reviewing for usability and accessibility problems.
---

# /usability-audit — Structured Usability & Accessibility Review

Takes a prototype (Track A or Track B), a live screen, or a flow, and returns a structured
issue list. Systematic and boring on purpose — this is the pass that catches the problems
everyone stops seeing after looking at a design for a week.

This is **objective evaluation against known rules**. Subjective, persona-specific
reactions belong in `/impersonate`; the two are complementary and often run together.

## Step 1 — Scope

Ask, batched, with the usual escape hatch:

1. **What am I auditing?** Repo path, running URL, artifact, or screenshots.
2. **What's the task** the user is trying to complete? Flow-level issues are invisible
   without a task.
3. **Who's the audience** — a persona document, or a segment description?
4. **Platform and constraints** — mobile/desktop, target accessibility standard
   (WCAG 2.2 AA is the sensible default), supported browsers.
5. **What's out of scope** — known issues, deliberate decisions not to relitigate.

If auditing a repo, read the actual component code, not just rendered output — focus
management, ARIA, and semantics live in the source. If auditing a URL, drive it in the
browser and interact with it; a screenshot cannot tell you whether tab order is broken.

## Step 2 — Run the passes

Run all four. Don't stop at the first pass that finds problems.

### Pass 1 — Heuristic evaluation (Nielsen's 10)

Visibility of system status · Match to the real world · User control and freedom ·
Consistency and standards · Error prevention · Recognition over recall · Flexibility and
efficiency · Aesthetic and minimalist design · Help users recognize and recover from
errors · Help and documentation.

For each, check the actual interface. Name the specific violation, not the heuristic in
the abstract.

### Pass 2 — Accessibility

- **Contrast** — text against its actual background, at its actual size and weight.
  Compute the ratio; state it. 4.5:1 body, 3:1 large text and UI components.
- **Text alternatives** — images, icon-only buttons, charts. Decorative images correctly
  hidden.
- **Labels** — every input programmatically associated with a visible label. Placeholder
  is not a label.
- **Focus** — visible focus indicator on every interactive element; logical tab order;
  no keyboard traps; focus moved and restored correctly on modals and route changes.
- **Semantics** — real headings in real order, landmarks, lists as lists, buttons as
  buttons (not divs with click handlers).
- **State communication** — errors, loading, and status changes announced to assistive
  tech, not signalled by color or position alone.
- **Motion and target size** — reduced-motion respected; touch targets at least 24×24 CSS
  px, ideally 44×44.

### Pass 3 — Flow level

- Dead ends, and states with no way back
- Steps that could be removed, merged, or deferred
- Data asked for before its value is established
- Irreversible actions with no confirmation, and reversible ones with unnecessary friction
- Missing states — empty, loading, error, partial, offline, permission-denied
- Error recovery that dumps the user back to the start
- Re-entry: what happens if they leave halfway and come back

### Pass 4 — Content

- Labels that describe the system rather than the user's intent
- Jargon, unexplained acronyms, internal vocabulary
- Error messages that state a code instead of a remedy
- Buttons whose labels don't say what happens next
- Copy that pads without informing

## Step 3 — Report

```markdown
# Usability audit: <what was audited>

**Scope.** <what was covered> · **Task.** <the task evaluated> · **Standard.** <e.g. WCAG 2.2 AA>
**Not covered.** <what wasn't audited, and why — never let scope be implied>

## Issues

| # | Severity | Location | Issue | Rule violated |
| :-- | :-- | :-- | :-- | :-- |
| 1 | Blocker | `Checkout.tsx:112` | Submit is a `div` with onClick — unreachable by keyboard | WCAG 2.1.1 Keyboard |

### 1. <Issue title>
**Observed.** <what is actually there>
**Where.** <file:line, or screen and element>
**Why it's a problem.** <the user consequence, concretely>
**Rule.** <heuristic or WCAG criterion>
**Fix.** <specific and actionable — the change, not the aspiration>

<repeat, severity descending>

## What's working
<genuinely — 2–4 items. A report with no positives gets discounted wholesale.>

## Recommended order
<the fix sequence by impact-to-effort, so the list is actionable on Monday>
```

Severity scale (shared with `/design-consistency` and `/drift-check`):

- **Blocker** — task cannot be completed, or an outright accessibility failure
- **Major** — completable, but with significant friction, error, or confusion
- **Minor** — noticeable roughness, no measurable task impact
- **Polish** — cosmetic or consistency nit

## Delivery

Before finalizing, ask where the output should go — a short menu, not a blocking gate:

- **Markdown file** at a path they name — recommend `audits/usability-<feature>.md`
- **Claude artifact** — a shareable, published page
- **Issues filed in the tracker** — one per finding, severity mapped to your labels
- **Confluence / Google Drive / Notion** — only if such a connector is actually attached
- **Terminal only**

If the user opts out of choosing, write the markdown file at the recommended default and
say plainly where you put it.

## Failure modes to avoid

- **Assuming a destination.** Never decide on the user's behalf where output lands. Ask.
- **Issues without fixes.** Every issue gets a concrete suggested fix. No exceptions.
- **Heuristic name-dropping.** "Violates consistency and standards" says nothing. Name the
  two places that disagree.
- **Auditing a screenshot and claiming keyboard coverage.** Say what you couldn't check.
- **Severity inflation.** If everything is a Blocker, nothing gets fixed first.
- **Relitigating deliberate decisions.** Respect the declared out-of-scope list.
