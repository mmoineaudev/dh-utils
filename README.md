# DH-Utils — Downhill Skateboarding for Deaf Riders

Design-thinking process repo for finding a way to enable deaf friends to do downhill
skateboarding/longboarding. This is a joined project with a few friends; the project
owner remains the **sole operator** for designing the technical solution. Friends act
as co-designers and domain witnesses (they ride, they know the conditions) — they are
not process editors.

## Ground rules (this project)

- **Docs-only for now.** Every phase produces markdown. No code, no builds, until
  the process says so.
- **Commit only when the owner says to.** Never auto-commit.
- **Domain truth comes from the owner.** Public sources on downhill skateboarding are
  scarce; specifics (security process, speeds, edge cases, gear, boards) must be
  extracted from the owner during phase 1.
- **AI role:** drive the process, ask the questions, write the docs. Owner steers and
  supplies ground truth; friends contribute user/domain input.

## The 7 phases

Value is **transitive from 0 to 6**: each phase stands on all the previous ones.
Phase 0 is the foundation and the most important part — if it's wrong, everything
downstream is built on a wrong premise. Later phases may be iterated on, but a
revisit of phase 0 invalidates more than any other step.

| # | Phase | Artifact |
|---|-------|----------|
| 0 | Frame | `00-frame.md` |
| 1 | Empathize | `01-empathize.md` |
| 2 | Define | `02-define.md` |
| 3 | Ideate | `03-ideate.md` |
| 4 | Prototype | `04-prototype.md` |
| 5 | Test | `05-test.md` |
| 6 | Deliver / systemize | `06-deliver.md` |

### 0 — Frame
One-sentence problem (goal, not a pre-baked solution), stakeholders and roles, hard
constraints, success criteria, explicit out-of-scope, and the list of open questions
to extract from the owner. Everything downstream inherits from this doc — keep it
short and keep it right.

### 1 — Empathize
Understand the people, not the tech. Jobs-to-be-done, pains, fears, current
workarounds, edge cases. Here, extraction sessions with the owner (security process,
speeds, gear, boards, the specific situations a deaf rider hits) plus friend
contributions. Verbatim where possible.

### 2 — Define
Synthesize into a crisp problem statement, "how might we" questions, the
failure-mode / edge-case matrix, and must-have vs nice-to-have.

### 3 — Ideate
Diverge wide before filtering: candidate solutions, cross-domain analogies,
constraint relaxation, invert-the-problem. Cluster, kill the weak, keep a shortlist.

### 4 — Prototype
Cheapest possible version of each shortlisted idea that can be evaluated. Fidelity
scales up only once an idea survives.

### 5 — Test
Put prototypes in front of the users; measure against the phase-0 success criteria;
record what worked, broke, or was misread.

### 6 — Deliver / systemize
End-to-end documentation of the final solution: how it's built/run, who's trained,
how it's maintained, so the friends can use and teach it without the owner.

## Iteration (going back is part of the method)

The flow is not a waterfall. Legal back-edges:

- **3 → 1** — ideation revealed an assumption about the users is wrong
- **3 → 2** — the problem statement itself needs revisiting
- **4 → 3** — a prototype can't be built the way ideation assumed
- **4/5 → 2** — testing exposed an unhandled failure mode / mis-defined problem
- **4/5 → 3** — testing killed the shortlisted idea; need to re-diverge

Any later phase may expose a defect in an earlier one. Because value is transitive,
a back-edge to phase 0 is the most expensive: treat it as a reframe, not a tweak.

## Conventions

- One file per phase, numbered `NN-name.md`, at the repo root.
- Every doc records its **status** (draft / agreed) and the **decisions** taken,
  so back-edges leave an audit trail instead of silently overwriting history.
- When a phase is re-entered, append a `## v2 — <date>` section rather than rewriting.
- Plain prose over jargon. No filler.
