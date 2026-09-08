---
name: spec-redline
description: Track B dev handoff — turns a low-fi prototype or flow description into an engineering-ready spec with redlines, component documentation, states, behaviors, edge cases and acceptance criteria. Use when a low-fi prototype (from /quick-proto) or a described flow needs to be documented in enough detail for engineering to build it.
---

# /spec-redline — Track B: Spec & Redline Generation

Low-fi prototypes are illustrative, not implementation-ready. They deliberately say
nothing about visual detail, and they leave most behaviour implicit. This skill closes
that gap by documenting a Track B prototype in engineering-ready detail.

For in-repo Track A prototypes, use `/handoff-pr` instead — those need no spec, because
the code is the spec.

## Step 1 — Gather

Ask, batched, with the usual escape hatch:

1. **What's the source?** A `/quick-proto` output, screenshots, a described flow.
2. **Is there a design system** to reference? If a codebase is accessible, read it and
   spec against real components by name — that removes most of the interpretation gap.
3. **Who's building this,** and how much context do they already have?
4. **What's already decided vs. still open?**
5. **Real data shape** — what does the API actually return, if known?

Read the prototype thoroughly first. Then, critically: **identify what it doesn't
specify.** A low-fi prototype leaves most behaviour implicit, and the gaps are exactly
where engineering will either guess or block. Enumerate them and ask about the ones that
matter, rather than silently inventing answers.

## Step 2 — Spec every layer

### Layout & structure
Per screen: regions, hierarchy, what's fixed vs. scrolling, responsive behaviour at each
breakpoint, overflow and truncation rules. Reference real design-system components by
name where one exists — never re-describe a component the team already has.

### Every state
The layer low-fi prototypes most often skip, and the one that consumes the most
engineering time when it's missing. For each screen and each component:

Default · Empty (first-use vs. filtered-to-nothing — usually different) · Loading (initial
vs. refresh vs. pagination) · Partial · Error (network, validation, permission, server) ·
Success · Disabled · Read-only · Offline · Long-content and overflow

If a state isn't specified, say so explicitly rather than leaving a silent hole.

### Behaviour
Every interactive element: what it does, what happens while it's happening, what happens
on success, what happens on failure. Validation rules and timing. Navigation and back
behaviour. Unsaved-changes handling. Focus management. Keyboard operation. Optimistic vs.
pessimistic updates. Debounce and throttle where relevant.

### Content
Exact copy for every label, button, heading, helper text, empty state, and error message.
Not approximate — exact. Include character limits and truncation rules, number/date/
currency formatting, and pluralization. Where copy is a placeholder, mark it clearly as
needing a content owner.

### Data
What each screen needs, where it comes from, what's required vs. optional, sort and
filter defaults, pagination approach, caching and refresh expectations.

### Accessibility
Heading structure, landmarks, labels, focus order, keyboard shortcuts, announcements for
dynamic content, contrast requirements, touch target sizes. Specify it — don't leave it
to be retrofitted.

### Redlines
Spacing, sizing, and alignment — **always in design tokens where they exist**, never raw
pixel values. If no token system exists, use a consistent scale and say which. If the
source is grayscale low-fi, state plainly that visual styling is unspecified and needs
design input rather than inventing values.

## Step 3 — Write it

```markdown
# Spec: <feature>

**Source.** <prototype reference> (Track B — low-fi) · **Design system.** <reference or "none">
**Status.** Draft | Reviewed · **Open questions.** <count>

## Overview
<what this is, who it's for, what problem it solves — 3–5 sentences>

## User flow
<numbered steps, including branches and failure paths>

## Screens

### <Screen name>
**Purpose.** <one line> · **Entry from.** <where> · **Exits to.** <where>

**Layout.** <structure, components by name, responsive behaviour>

**Elements**
| Element | Component | Content | Behaviour |
| :-- | :-- | :-- | :-- |

**States**
| State | Trigger | Appearance | Copy |
| :-- | :-- | :-- | :-- |

**Data.** <what it needs and from where>
**Accessibility.** <headings, focus, labels, announcements>
**Redlines.** <spacing/sizing in tokens>

<repeat per screen>

## Edge cases
| Case | Expected behaviour |
| :-- | :-- |

## Acceptance criteria
- [ ] <testable, specific, verifiable by someone who wasn't in the room>

## Open questions
| # | Question | Blocks | Owner |
| :-- | :-- | :-- | :-- |

## Explicitly not specified
<what this spec deliberately leaves to engineering judgment — naming it prevents both
silent guessing and unnecessary blocking>
```

## Step 4 — Deliver

Ask where the spec should go:

- **Markdown file** at a path they name — recommend `docs/specs/<feature>.md`
- **A ticket** in the tracker — often right, since this is what engineering builds from
- **Claude artifact** — a shareable, published page
- **Confluence / Google Drive / Notion** — only if such a connector is actually attached
- **Terminal only**

If the user opts out of choosing, write the markdown file at the recommended default and
say plainly where you put it.

Then note the honest trade-off: this spec exists because the prototype was low-fi. If the
team has codebase access, `/design-proto` would have skipped most of this document
entirely. That's the Track A argument, made concrete by the length of what you just wrote.

## Failure modes to avoid

- **Assuming a destination.** Never decide on the user's behalf where output lands. Ask.
- **Happy path only.** The states table is the highest-value part of the spec.
- **Approximate copy.** "Something like 'no items yet'" becomes three different strings in
  production.
- **Inventing visual detail** the low-fi source never specified. Flag it as needing design
  input instead.
- **Raw pixel redlines** where a token system exists.
- **Untestable acceptance criteria.** "Works well on mobile" is not a criterion.
- **Silently filling gaps.** Ask about the ones that matter; list the rest under
  "explicitly not specified."
