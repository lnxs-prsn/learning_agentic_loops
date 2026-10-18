# Backbrief — learning_agentic_loops

## BB-1 — to BR-1 (install, package p1)
date: 2026-10-18
from: project agent (Claude Opus 5.5)

**The why, in my words.** This folder is where the owner keeps the multi-agent loops their other projects run on, and their thinking about how such loops should be designed. It stalled after one commit because nothing says which of those two it is for. The method is being installed so the project can be directed again, or put down on purpose, without the owner re-explaining it each session. So the next step isn't to build anything. It's to make the aim decision cheap and safe for the owner.

### 1. The aim, checked
The draft is mostly right. I corrected four things in `aim.md` (still `status: derived`, evidence cited):
- **Eight loop families, not seven.** `refactor_agents/` (9 files) was missing.
- **`data_to_improve_loops/` was misread.** It is not a revised copy of the planning loop but a *smaller* one: no `16_loop_health.md`, a runner of 383 lines against 576, four shorter files, and 12 identical ones. Probably it's the earlier version, kept as a baseline for improvement.
- **A known consumer.** `initial_build.md` is a delivery spec for **harnessv8** (every proof test runs in `/home/mr/Desktop/python/harness_design/harnessv8`). That makes it evidence of a copy, not just a sample.
- **Added C3b (C2 now, C1 kept usable).** The newest work here is design notes, not loops, and the notes keep naming "run this on one existing loop" as the next step. I also wrote down each candidate's likely first stage, so the owner is choosing between concrete next steps rather than abstractions.

Only the owner can settle which candidate, where else the loops went, and whether the notes file belongs in the repo.

### 2. Strategy briefing (BR-2, written into `brief.md`)
- **Context.** *Known:* a library of 8 loop families plus design notes, in hiatus. harnessv8 used the delivery loop. The notes file was untracked until the tool's before commit, and `main` tracks a GitHub remote. *Probable:* the owner's live interest is loop design, and the loops' real results sit in the copying projects. *Unknown:* the aim, the other copies, and whether the notes were kept out of git deliberately.
- **Higher intent.** One level up, the owner wants a project that can be directed, or archived on purpose. Two levels up, their other projects run on these loops. If the owner were here, they'd want one cheap decision, nothing published by surprise, and no work started toward an aim nobody picked.
- **Current intent.** Put the aim to the owner as a one-screen choice, and clear the outward risk the install created, *in order to* stop guessing. Wrong guesses here are paid for by every project that copies a loop.
- **Main effort.** The owner's aim decision (ST-1). My part is done in `aim.md`. Cut last.
- **Implied tasks.** Report NOTICE and the push risk, then seed a copies list, then a README after the aim is set. Nothing touches the loops before an aim exists.
- **Freedoms / constraints.** I can read this repo, write the package, add new files and commit locally after acceptance. I won't edit loop files, `fiction/`, `data_to_improve_loops/` or the owner's top-level files. I won't push or rewrite history, and I won't read harnessv8 without permission.

### 3. Mapping onto existing practice
The project has **no operating practice of its own**: no handoff, tickets, decision log, tests, hooks or gates. CLAUDE.md came with the install. So the method replaces nothing. It *is* the project's first operating layer.
- **Complements:** `insights_for_loops.md` stays the owner's design notebook. Under C2/C3b its "Open decisions" and "How to test it" sections become stage material in `aim.md`. The method doesn't absorb the notes.
- **Binding tactics:** git as found, plus the tool's before/after commit discipline (never push, never revert a before commit). Commit format: the project has none, so I'll use the tool's.
- **The loops are product, not practice.** Their runner tables, verdict tokens, 3-cycle caps and "call the Boss" rules are tactics *inside the product* and stay untouched. The vocabulary overlaps, and the overlap is worth recording for C2. Loop "Boss" ≈ the level that resolves what a brief can't. Gate, regression and story validators ≈ controls (METHOD §9). `16_loop_health` ≈ a dashboard. The Planner's CONFLICT_MANIFEST ≈ a backbrief. Two things don't map. The loops carry the *how* in detail and leave the *why* outside the agents, which insight 7 already argues for. And none of them has a backbrief step. Both are candidate C2 experiments, not install work.

### 4. Proposals
- **PR-1 (entry file): adapted.** Accept the README, but write it *after* the aim is picked, in the same session. A README written now could only say "purpose: open", and the repo is on GitHub, so that would be a public statement made before the owner decides. Content: one line from the aim, the state, a map of the 8 families + fiction + notes, and a pointer to `aim.md`. About 15 lines.
- **PR-2 (record copies): adapted.** Put the list in `.directed_opportunism/copies.md`, not the README. Local paths of the owner's other projects don't belong on a public front page. I'd seed it with harnessv8 ← delivery_agents (evidence: initial_build.md), and the owner fills in the rest. It's needed only under C1/C2/C3/C3b; skip it if the owner archives.

### 5. Conflicts
1. **The install swept the owner's untracked notes into git, on a branch that tracks GitHub.** `insights_for_loops.md` was untracked. That may have been deliberate: it includes remarks on the owner's job search and another project, and it ends in an empty "insight 8". The tool's before commit ff3c978 now holds it, so the next `git push` publishes it. No history has been pushed yet, so this is easy to fix now. *Resolution:* the owner decides. Either keep it, or remove it before pushing, which means changing ff3c978, since `git rm --cached` alone still leaves it in history. That's a history rewrite, so I do it only on explicit instruction.
2. **Control-loop overhead against a hiatus project.** With `tight`, every work cycle needs a self-audit and every non-trivial task a backbrief. For a folder that may see one session a month, that's the "form" METHOD warns about. *Resolution:* write audits only for cycles where something changed, and keep `tight` until the first post-aim cycle.
3. **No existing Bungay summary or rule here contradicts the method.** The closest thing is insight 7 ("agents carry no why… the selection loop supplies the purpose from outside"), which agrees with it.
4. **Wording:** the aim draft said "seven" loops and "revised copy". Both are fixed (§1).

### 6. Integration plan (after acceptance; small first, where the risk is)
1. **Owner:** decide about `insights_for_loops.md` before any push. I execute only the option they name.
2. On the owner's acknowledgement of NOTICE: delete `.directed_opportunism/NOTICE.md` and commit.
3. **Owner picks the aim** → I mark AIM-1 `confirmed` with the owner's words and the date (or write AIM-2 if they correct it), draft the stages for that candidate, write BR-3, and backbrief it.
4. Create `.directed_opportunism/copies.md` seeded with harnessv8 (PR-2).
5. Create root `README.md` (PR-1).
6. `config.json`: `install_state` → `integrated`. CLAUDE.md already points here, so it needs no change.
Each step is its own local commit. Nothing is pushed, and no loop file changes. If the owner picks *archive*, steps 4–5 shrink to a README that says archived and lists where the copies live.

### 7. What I can't do / disagree with
- I can draft and sharpen the candidates, but **not pick the aim**. That's the owner's.
- I can list harnessv8 as a copy, but **not the other copies or how they fared** unless the owner tells me or lets me read those projects.
- I can say the `data_to_improve_loops/` copy is smaller, but **not prove it's older**: one commit, no history.
- **I partly disagree with BR-1's framing** of "C1 now, C2 next" as the natural middle option. The evidence leans the other way (C3b), so I added it rather than let C3 stand as the default.
- **I disagree with a self-audit per cycle at this stage** (Conflict 2). Writing it when nothing happened would be form-filling.

### 8. Questions for the owner
1. **Which aim: C1, C2, C3, C3b or archive (or a correction)?** Stage ST-1 · impact: changes-aim · why: everything after this depends on it, and the evidence supports more than one.
2. **`insights_for_loops.md`: keep it in the repo, or take it out before you push?** Stage: none · impact: untouched (aim), but outward and hard to undo once pushed · why: it was untracked, the install committed it, and `main` tracks GitHub. *Answer this before your next push.*
3. **Which projects copied which loops, beyond harnessv8? Or may I read them to find out?** Stage ST-1→next · impact: advances (C1/C2/C3/C3b) · why: the loops' real results live there, and I can't see outside this repo without permission.
4. **Is `data_to_improve_loops/` the earlier planning loop kept as a baseline?** Stage: next · impact: route-only · why: under C2 it decides whether the first experiment compares the two versions.

### Situation check
Changed since BR-1: three facts the brief didn't have (a known consumer, the direction of the planning-copy difference, the public-push risk). None of them invalidates BR-1. They are folded into BR-2.
