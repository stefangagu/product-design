# Cross-Cutting Interaction Principle

Every skill in this repo follows the same information-gathering contract. This exists so
skills stay fast for people who don't have every detail on hand, without silently
degrading output quality.

## The contract

1. **Ask, don't assume.** When a skill needs information to do its job properly, ask the
   user directly. Do not silently invent a target user, a business goal, a constraint, or
   a success metric.

2. **Always offer the escape hatch.** Every question must make it obvious the user can
   reply with "idk for now" or "take your best guess." Never block on an answer.

3. **If the user opts out, state confidence.** Proceed with a best guess, but label the
   assumption explicitly so the user knows which parts of the output are grounded and
   which are inferred.

4. **Batch questions.** Ask everything you need in one pass (numbered), not one question
   per turn. Three to six questions is the normal range; more than eight means the skill
   is asking for things it should infer.

## Confidence labelling

Use these three labels, consistently, everywhere confidence is reported:

| Label | Means |
| :-- | :-- |
| **Grounded** | Stated by the user, or read directly from the codebase / a cited source. |
| **Inferred** | Derived from something grounded, by reasonable reasoning. Say what it was derived from. |
| **Assumed** | A best guess with no supporting input. Say what would change it. |

Inline form: `[Grounded]`, `[Inferred — from the codebase's existing checkout flow]`,
`[Assumed — no analytics provided; a funnel export would confirm or kill this]`.

## Mandatory confidence output

`/research`, `/persona`, and `/impersonate` must include confidence labels as a **standard
part of every output** — not only when a guess was made. For those three skills, an output
with no confidence annotation is an incomplete output.

## Sourcing rule (applies to /research and /research-synthesis)

Every factual claim carries a real, verifiable source: a URL, a document name, a
transcript ID, a dashboard, a line of code. No fabricated citations, no vague
attributions ("studies show", "industry research suggests"). If a claim cannot be backed
by a real source, mark it `[Unverified]` and present it as a hypothesis, never as fact.

## Delivery-destination rule (applies to /research and /persona)

Before finalizing, ask where the output should go. Offer at minimum:

- A markdown file at a path the user names (recommend a sensible default path)
- A Claude artifact
- Confluence / Google Drive / Notion — only if such a connector is actually attached
- Just print it in the terminal

If the user opts out of choosing, write a markdown file next to the project and say where
you put it.

> A shared Product Knowledge Repo — a persistent store all these skills read from and
> write to — is the intended long-term home for these outputs. It is deliberately not
> built yet; skills must work standalone until it exists.
