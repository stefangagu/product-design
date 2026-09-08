---
name: persona
description: Guided persona builder — runs a structured intake questionnaire, presents the persona back for confirmation, then writes it out as a reusable document to a destination the user chooses. Personas built here are the input for /impersonate. Use when the user wants to create, document, or refine a user persona.
---

# /persona — Guided Persona Builder

A persona is a research deliverable, not a role-play prompt. This skill produces a
document that gets stored, referenced, revised, and loaded later by `/impersonate`.

## Non-negotiables

1. **Confidence labels on every trait** — mark each field `[Grounded]` (the user told us,
   or it came from research), `[Inferred]` (derived from something grounded), or
   `[Assumed]` (a best guess). This is the single most important property of the output:
   whoever uses the persona later needs to know which traits are real.
2. **Ask where the document goes** before writing it.
3. **Never invent a persona wholesale** and present it as researched. If the user has no
   inputs, say plainly that this is a proto-persona built on assumptions and that it
   should be validated before it drives decisions.

## Step 1 — Intake

Ask these as one numbered batch. Tell the user explicitly they can answer some, skip
others with "idk for now," or say "take your best guess" for the whole thing.

**Identity & context**
1. Name, age range, location, living/working context
2. Role or job title, and what they're actually accountable for
3. Industry / company size / life stage, as relevant

**Behaviour & capability**
4. Tech literacy — what they use comfortably, what they avoid
5. Devices and contexts of use — mobile on the move, desktop at a desk, shared device, low connectivity
6. Relevant existing habits and tools, including the workarounds they've built

**Motivation**
7. Goals — what they're trying to accomplish, in their words not the product's
8. Jobs to be done — the circumstance that makes them reach for a solution
9. What "good" looks like to them — how they'd know it worked

**Friction**
10. Frustrations and pain points with the current way
11. Anxieties, risks, and what they're afraid of getting wrong
12. What would make them abandon or distrust the product

**Decision-making**
13. Who else is involved in their decision — approvers, influencers, dependents
14. What they need to see before they'll commit
15. Where they currently go for information and recommendations

**Grounding**
16. What is this persona based on? (Interviews, analytics, sales conversations, a
    stakeholder's opinion, or nothing yet.) This determines the honest confidence ceiling
    for the whole document.

Ask follow-ups only where an answer is load-bearing and genuinely unclear. Do not
interrogate.

## Step 2 — Play it back

Before writing anything, present the persona as an organized bulleted summary with
confidence labels visible, and ask for confirmation or corrections. Explicitly point at
the weakest inferred/assumed traits and ask if they look right — those are where the
persona will mislead if wrong.

## Step 3 — Write the document

```markdown
# Persona: <Name> — <one-line positioning, e.g. "Time-poor ops lead at a 40-person agency">

**Based on.** <what grounds this persona> — **Overall confidence.** Grounded | Mixed | Speculative
**Created.** <date> · **Last revised.** <date>

## At a glance
> <2–3 sentence narrative. Written as a person, not a spec sheet.>

## Identity
- **Age / location / context** — <value> `[Grounded]`
- **Role** — <value> `[Grounded]`
- **Accountable for** — <value> `[Inferred — from role]`

## Behaviour
- **Tech literacy** — <value> `[label]`
- **Devices & contexts** — <value> `[label]`
- **Current tools & workarounds** — <value> `[label]`

## Goals & jobs to be done
- **Primary goal** — <value> `[label]`
- **JTBD** — When <circumstance>, I want to <motivation>, so I can <expected outcome> `[label]`
- **Definition of success** — <value> `[label]`

## Frustrations
- <value> `[label]`

## Anxieties & deal-breakers
- <value> `[label]`

## Decision context
- **Others involved** — <value> `[label]`
- **Needs to see before committing** — <value> `[label]`
- **Information sources** — <value> `[label]`

## How to use this persona
**Reliable for.** <the decisions this persona is grounded enough to inform>
**Not reliable for.** <where it's guessing and shouldn't be leaned on>
**To strengthen it.** <the specific research that would convert Assumed traits to Grounded>

**Confidence summary**
- Grounded: <traits>
- Inferred: <traits, and from what>
- Assumed: <traits, and what would confirm them>
```

## Step 4 — Deliver

Ask the destination — markdown file at a path they name (recommend one), Claude artifact,
Confluence/Drive/Notion if a connector is attached, or terminal only. Then tell them the
persona can be loaded by `/impersonate` to get in-character feedback on concepts, flows,
and screens.

## Revising an existing persona

If a persona document already exists, load it and work as a diff: what's changing, what
evidence drives the change, which confidence labels are being upgraded or downgraded.
Keep the old version rather than overwriting silently — a persona that shifted is itself
a finding.

## Failure modes to avoid

- **Demographic theatre.** Age, a stock-photo vibe, and a favourite coffee order tell you
  nothing about a design decision. Behaviour, motivation, and constraints do.
- **The persona who wants your product.** If the persona's goals map one-to-one onto your
  feature list, it's a sales sheet wearing a persona costume.
- **Uniform confidence.** A document where every trait reads equally certain is one that
  will be trusted equally everywhere — including where it's guessing.
