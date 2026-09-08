# Claude Skills for Design & Product Workflows

A set of Claude Code skills that map AI onto the real product design pipeline — from
research through to shipped product — built for a workshop on how AI can improve design
and product processes.

Each skill is a self-contained slash command. Run `/research`, `/persona`, `/design-proto`
and so on from Claude Code inside a project.

## The pipeline

```
Research → Ideation → Prototyping → Validation → Dev Handoff → Shipped Product
                                                       ↓
                                    Design System Governance (feedback loop)
```

## The skills

| Stage | Skill | What it does | Primary user |
| :-- | :-- | :-- | :-- |
| **1. Research** | `/research` | Product-oriented research framed around decisions and hypotheses, with real sources | Designers / Researchers |
| | `/research-synthesis` | Raw transcripts, surveys and tickets → structured themes and persona updates | Designers / Researchers |
| | `/persona` | Guided persona intake → confirmed summary → reusable persona document | Designers / PMs |
| **2. Ideation** | `/ideation` | Divergent concept directions from a brief, plus A/B copy and layout variants | Designers / PMs |
| **3A. Prototyping** | `/design-proto` | High-fidelity prototyping **in the real codebase** with the real design system | Designers |
| **3B. Prototyping** | `/quick-proto` | Fast, grayscale, style-agnostic flow prototypes — no codebase needed | PM / PO / BA |
| **4. Validation** | `/usability-audit` | Heuristic + accessibility + flow audit with severity and concrete fixes | Designers |
| | `/impersonate` | Loads a persona and gives in-character feedback on concepts, flows or screens | Designers / PMs |
| **5. Design System** | `/design-consistency` | Audits the real app for component, typography, color and behavioral inconsistency | Designers / Eng |
| | `/drift-check` | Compares what shipped against the design mock it came from | Designers / Eng / PM |
| **6A. Handoff** | `/handoff-pr` | Packages an in-repo prototype as a PR-ready review package | Designers / Eng |
| **6B. Handoff** | `/spec-redline` | Turns a low-fi prototype into an engineering-ready spec with redlines | Designers |

## The two prototyping tracks

The core differentiator, and the part worth spending workshop time on.

**Track A — `/design-proto`.** Designers work directly in the frontend codebase, using the
real, shipped design system. Prototypes are accurate to what will actually ship, not
approximations of it. Requires live repo access via Claude Code.

**Track B — `/quick-proto`.** A skill encoding core UX best practices for PMs, POs, BAs and
other non-designer roles. Rough-but-sound grayscale prototypes, no design tool proficiency
required. Intentionally illustrative, never implementation-ready.

They diverge again at handoff, and that divergence is the real argument:

- **From Track A**, handoff is near-zero-translation — `/handoff-pr` produces a branch to
  review, not a spec to build from. The code *is* the spec. Days of redlines compress into
  a normal code review cycle.
- **From Track B**, a full spec is still required — `/spec-redline` writes it. The length
  of that document is itself the case for Track A.

Track A isn't just "more accurate mocks." It's a structural fix to the handoff bottleneck,
not an incremental improvement to a deliverable.

## Shared conventions

Every skill follows the same contract, documented in `shared/`:

- **[`interaction-principle.md`](shared/interaction-principle.md)** — ask rather than
  assume; always let the user say *"idk for now"* or *"take your best guess"*; when they
  do, proceed but state confidence explicitly. **Every skill asks where to deliver its
  output** — markdown file, artifact, connector, tracker, or terminal — and never picks a
  destination on the user's behalf. `/research`, `/persona` and `/impersonate` additionally
  carry confidence labels in **every** output as standard, and `/research` must always cite
  real, verifiable sources.
- **[`output-formats.md`](shared/output-formats.md)** — shared shapes so outputs compose:
  insight → implication → recommendation, a common severity scale across all three audit
  skills, option sets, and the confidence block.

## Repo layout

```
skills/     the 12 skills, one directory each, containing a SKILL.md
shared/     conventions every skill follows
.claude/    a symlink pointing at skills/, so Claude Code loads them automatically
```

The skills live in the plain `skills/` directory so they're easy to browse and share.
`.claude/skills` is a symlink to it — that's the path Claude Code reads from, so cloning
this repo and opening it gives you all 12 working immediately, with nothing to copy.

## Using these skills

Open this repo in Claude Code and the skills are live — invoke one by name (`/research`)
or let it be picked up automatically when a task matches.

To use them in another project, copy the `skills/` directory to `.claude/skills/` there,
or copy individual skill folders — each `SKILL.md` is self-contained.

Two skills need live codebase access — `/design-proto` and `/design-consistency` — and
`/drift-check` needs it for Track A comparisons. Everything else works standalone.

## Not built yet

**Product Knowledge Repo** — a persistent, structured store that all these skills read
from and write to, so research, personas, decisions, audits and handoff artifacts compound
across projects instead of being one-off outputs. Deliberately deferred; every skill works
standalone until it exists, and each one asks where to deliver its output rather than
assuming a repo is there.

Open questions for the workshop:

- Which skills to build out first — highest leverage vs. lowest effort?
- What the Product Knowledge Repo's structure and schema should actually be
- Where Track A needs guardrails, so prototype code isn't mistaken for production-ready
- How success gets measured — time saved, handoff cycle time, defect rate, adoption
