# Shared Output Formats

Consistent shapes so outputs from different skills compose instead of collide.

## Insight → Implication → Recommendation (research, synthesis)

```markdown
### <Short insight title>

**Insight.** What is true, stated as a finding. [Grounded — <source>]

**Implication.** What that means for this product specifically. Not a generic truism.

**Recommendation.** What to do about it, concretely enough to act on this sprint.

**Confidence.** Grounded | Inferred | Assumed — plus the one thing that would raise it.
**Sources.** <real, verifiable references>
```

## Issue list (usability audit, consistency audit, drift check)

One table, sorted by severity descending, then a details section per issue.

| # | Severity | Location | Issue | Heuristic / rule violated |
| :-- | :-- | :-- | :-- | :-- |

Severity scale, used identically by all three audit skills:

- **Blocker** — users cannot complete the task, or it fails an accessibility requirement outright.
- **Major** — users complete the task but with significant friction, error, or confusion.
- **Minor** — noticeable roughness, no measurable task impact.
- **Polish** — cosmetic or consistency nit.

Each detail entry carries: what was observed, where (file:line or screen name), why it's a
problem, and a concrete suggested fix. No fix suggestion, no issue — an audit that only
complains is half an audit.

## Option set (ideation, A/B variants)

Numbered options, each with a name, a one-line description, and an explicit rationale.
Options must be genuinely different bets, not the same idea reworded. Close with a short
"how these differ" note naming the axis they vary along.

## Confidence block (research, persona, impersonate)

Every output from those three skills ends with:

```markdown
**Confidence summary**
- Grounded: <what came from the user or a real source>
- Inferred: <what was derived, and from what>
- Assumed: <what was guessed, and what would confirm it>
```
