---
name: impersonate
description: Load a persona built with /persona and give simulated in-character feedback on concepts, flows, prototypes, or shipped features. Reports friction, confusion and drop-off points from that persona's point of view, with explicit confidence about how well the persona's defined traits actually support each reaction. Cross-stage — usable in ideation, prototyping, validation, or retrospectively.
---

# /impersonate — Persona-Driven Feedback

Loads a saved persona and reacts to what you show it, in character. Most commonly used on
screens and prototypes, but it is a cross-stage tool: the same loaded persona can react to
an early concept during ideation, a prototype during validation, or a shipped feature in a
retro.

## Non-negotiables

1. **Confidence on every reaction.** State how well the persona's *defined traits* support
   each piece of feedback. A reaction grounded in a documented frustration is worth acting
   on; a reaction extrapolated from nothing in the persona is noise wearing a costume.
2. **This is not user testing.** It is a cheap, fast, structured pre-filter that catches
   obvious problems before real people spend their time on them. Say this once at the
   start of a session and never oversell the output.
3. **Never invent traits mid-session.** If a reaction would require something the persona
   document doesn't say, flag the gap instead of filling it: "the persona doesn't specify
   X — if X is true, this would be a blocker; if not, it's fine."

## Step 1 — Load

1. If the user named a persona, load that document. Otherwise list available personas and
   ask which to load. If none exist, offer to run `/persona` first.
2. Read the full document, including the confidence labels — they set the ceiling on how
   confidently this session can react.
3. Confirm the load back to the user, compactly:

> Loaded **<Name>** — <one-line positioning>.
> Grounded traits: <list>. Assumed traits: <list> — reactions leaning on those will be labelled low-confidence.
> Show me the screens, flow, or concept and I'll give simulated feedback as <Name>.

Also ask, briefly, for the **task context**: what is this persona trying to accomplish
here, and where did they arrive from? Reactions without a task are just opinions.

## Step 2 — React

Stay in character for the reaction, then step out for the analysis. Two clearly separated
registers — never blur them.

For a **flow or prototype**, walk it step by step:

```markdown
## <Name> walks through <flow>

### Step 1 — <screen/state>
> *In character:* "<what they notice first, what they expect, what they'd do, what confuses them>"

**Friction.** <what actually goes wrong, named>
**Severity.** Blocker | Major | Minor | Polish
**Why this persona specifically.** <the documented trait driving it — quote the persona doc>
**Confidence.** High — <trait> is grounded in the persona | Medium — inferred from <trait> | Low — the persona doesn't define <X>; this is extrapolation

<repeat per step>

### Where <Name> drops off
<the most likely abandon point, and what would have to change to prevent it>

### What worked
<genuinely — a critique-only pass is not a useful signal>

**Confidence summary**
- Grounded reactions: <which, and the traits behind them>
- Inferred reactions: <which, and what they were derived from>
- Extrapolated / unsupported: <which — treat as hypotheses, not findings>
```

For a **concept** (no screens yet), react to the pitch: would this persona care, would
they understand it, what would they compare it to, what would stop them adopting it.

## Step 3 — Deliver and persist

Sessions are worth keeping — a persona's reaction is evidence, and it compounds across
rounds of a design.

Ask where the session write-up should go:

- **Markdown file** at a path they name — recommend `research/impersonate-<persona>-<flow>.md`
- **Claude artifact** — a shareable, published page
- **Appended to the persona document**, as a dated reaction log
- **Confluence / Google Drive / Notion** — only if such a connector is actually attached
- **Terminal only** — the right answer for a quick in-the-moment gut check

If the user opts out of choosing, write the markdown file at the recommended default and
say where you put it.

Then offer to fold anything learned back into the persona (via `/persona` in revise
mode) — for instance, a reaction that revealed a missing trait the persona should define,
or an assumed trait the session showed to be load-bearing enough to go and validate.

## Multi-persona passes

If several personas are relevant, run them separately and then compare: what all of them
hit is a design problem, what only one hits is a segment problem. Never merge personas
into a composite — the disagreement between them is the whole value.

## Failure modes to avoid

- **Assuming a destination.** Never decide on the user's behalf where output lands. Ask.
- **The agreeable persona.** A persona that likes everything is broken. Personas have
  goals; goals get frustrated.
- **Generic usability feedback in a wig.** If the reaction would be identical for any
  persona, it belongs in `/usability-audit`, not here. Every reaction should be traceable
  to a specific documented trait.
- **Confidence smuggling.** Never let a fluent in-character voice imply grounded evidence.
  The persona sounds certain; the confidence label tells the truth.
- **Stacking it against real testing.** This finds obvious problems fast. It does not
  find what you didn't think to ask about — only real users do that.
