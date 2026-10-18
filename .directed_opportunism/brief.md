# Strategy brief — learning_agentic_loops

METHOD §5 (book template p.249). Concepts to think with, not boxes to fill. Contains "all, but also only," what the receiver can't determine for themselves. Keep it to about one page.

---

## BR-1 — install directed opportunism in learning_agentic_loops
date: 2026-10-18
aim: AIM-1 (status: derived; open: candidates C1–C3)
status: draft
superseded_by: none

### 1. Context
- Known: a library of loop role prompts and design notes, in hiatus; no entry files (no README, CLAUDE.md or handoff before this install); no tests; the owner lets the tool take the planning role, but confirming the aim stays the owner's.
- Probable: the loops' best evidence lives in the projects that copied them.
- Unknown but relevant: which aim the owner picks.

### 2. Higher intent
- One level up: the owner wants this project to have a direction it can be worked toward, without having to explain the method.
- Two levels up: AIM-1 (once confirmed).

### 3. Current intent
**What:** adopt directed opportunism here and settle the direction
**in order to**
**Why:** a project in hiatus can't be directed until it has an aim; the first job is closing that knowledge gap (book p.110: intent before action), not producing loops.
Measures (dashboard, not goal): the owner can pick an aim in one sitting; the first strategy brief names one main effort.

### 4. Implied tasks
| Task | Owner | Timing |
|---|---|---|
| **Check the candidate aims against the project and sharpen them (the project's first strategy brief, BR-2)** (MAIN EFFORT) | project agent | install backbrief |
| Map the method onto the loop files' own concepts (runner, boss, gates) without changing them | project agent | install backbrief |
| Decide PR-1..PR-2 | project agent | install backbrief |
| Integration plan: small, entry files only | project agent | install backbrief |

### 5. Boundaries
- Freedoms: read everything; add, drop or reword candidate aims with evidence (the aim stays derived); propose the first stages for each candidate.
- Constraints: write only in `.directed_opportunism/` until accepted; **never edit the loop files or the owner's notes** (`*_agents/`, `fiction/`, `data_to_improve_loops/`, the three top-level .md files); never push.
- Anti-goals: don't pick the aim for the owner; don't invent a direction the evidence doesn't support; don't turn the install into a redesign of the loops.

### 6. Backbrief
Point: `.directed_opportunism/backbrief.md`, before any change outside the package.

---

## BR-2 — get learning_agentic_loops an aim, safely and cheaply
date: 2026-10-18
aim: AIM-1 (status: derived; open: candidates C1, C2, C3, C3b, archive)
status: draft (written by the project agent in BB-1; becomes active when the owner accepts the backbrief)
supersedes: BR-1 once the install is accepted
superseded_by: none

### 1. Context
- Known: a library of eight agentic-loop families (role prompts, no code, no tests) plus the owner's design notes; in hiatus since one commit (2026-07-11). At least one loop went to another project: initial_build.md is a delivery-loop spec for harnessv8. The planning loop exists in two versions; the kept copy in data_to_improve_loops/ is the smaller one. The design notes (insights_for_loops.md) are the newest work and were never committed until the tool's before commit ff3c978 swept them in. `main` tracks a GitHub remote, so the next push publishes those notes.
- Probable: the owner's current interest is loop *design* (the notes) more than adding loops; the loops' real results live in the projects that copied them.
- Unknown but relevant: which aim; where else the loops went; whether the notes were kept out of git on purpose.

### 2. Higher intent
- One level up: the owner wants this project to have a direction it can be worked toward, without explaining the method each time; it's in hiatus, so the direction may be "archive".
- Two levels up: the owner's other projects run on these loops; whatever this project becomes should make those loops better or easier to reuse, or get out of the way.
- So, if the owner were here and knew what I know: they'd want one cheap decision put in front of them, nothing published they didn't mean to publish, and no work started toward an aim they haven't picked.

### 3. Current intent
**What:** put the aim decision to the owner as a one-screen choice, and clear the one outward risk the install created (the notes file headed for GitHub)
**in order to**
**Why:** until the aim is picked, any work on the loops is a guess (knowledge gap), and the cost of the wrong guess falls on the projects that copy them.
Measures (dashboard, not goal): the owner picks or corrects an aim in one sitting; nothing is pushed that the owner hasn't seen; no loop file changes.

### 4. Implied tasks
| Task | Owner | Timing |
|---|---|---|
| **Owner decision on the aim (ST-1), made cheap: candidates checked and corrected against the files, each with its first concrete stage** (MAIN EFFORT) | project agent prepares (done in aim.md); owner decides | now |
| Report NOTICE.md; flag the insights_for_loops.md push risk | project agent | first thing to the owner |
| Record known copies (harnessv8 so far) | project agent seeds; owner completes | after acceptance |
| Entry file (README) | project agent | after the aim is picked |
| Everything else (loop changes, experiments) | — | not before an aim |

Cut order: README first, copies list second; the aim decision is cut last.

### 5. Boundaries
- Freedoms: read anything in this repo; write in `.directed_opportunism/`; after acceptance, add new files (README.md, a copies note) and commit locally; refine candidate aims with evidence.
- Constraints: don't edit loop files, `fiction/`, `data_to_improve_loops/` or the owner's top-level notes/specs; never push; never rewrite history (ff3c978 included) without the owner's explicit instruction; don't read other projects (harnessv8) without the owner's permission.
- Anti-goals: don't pick the aim for the owner; don't let the install publish the owner's private notes; don't turn a hiatus project into busywork (no audits for cycles where nothing happened).

### 6. Backbrief
Point: BB-1 in `backbrief.md` (this install); after the owner's aim decision, a short backbrief to BR-3 before the first stage starts.
