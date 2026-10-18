# Message log — tool ⇄ project agent — learning_agentic_loops

Append-only. Durable channel between the `directed_opportunism` tool and this project's agent (works with headless runs and survives sessions). Newest at the bottom. Timestamps read from the clock.

Format:
## MSG-<n> — <type: brief | backbrief | re-brief | review | question | answer | note>
date: <ISO timestamp>
from: <tool | project-agent | owner>
re: <ids>

<body>

---

## MSG-1 — answer
date: 2026-10-18T16:05:20+03:00
from: owner (relayed by the tool, from the install sitting)
re: backbrief.md BB-1 §8, AIM-1, NOTICE.md

1. **Aim:** "it's to become a factory for building agentic loops. All the loops it has currently have been used by many others, so they are example loops that the factory can reference when building future loops." Recorded as AIM-2, confirmed; AIM-1's candidates are superseded.
2. **insights_for_loops.md:** fine to go to GitHub; nothing important in it besides insights for the project. Keep it.
3. **Untracked files in general** (the tool's rule now): a file not in .gitignore is fair to commit; one that shouldn't go to git gets added to .gitignore, recorded in the notice.
4. **Copies:** at least two more projects besides harnessv8 used the loops; they were lost in a reinstall (never on GitHub). Don't search for them.
5. `data_to_improve_loops/`: the owner doesn't recall its origin.
6. NOTICE.md: seen (acknowledged). The tool deletes it with this commit.
7. Self-audits only for sessions where work happened: agreed.

## MSG-2 — accepted
date: 2026-10-18T16:05:20+03:00
from: tool
re: backbrief.md BB-1

BB-1 is accepted. It was a strong backbrief: it stated the why, corrected the draft in four verified places, disagreed with reasons, and caught the untracked-notes risk. The tool has recorded AIM-2 and deleted NOTICE.md (plan items 2–3, aim part).

Integration step: make plan items 4–6 now that the aim is confirmed:
- 4. `.directed_opportunism/copies.md`: harnessv8 ← delivery_agents (evidence: initial_build.md), plus "at least two more projects, lost in a reinstall" (MSG-1).
- 5. Root `README.md` (PR-1): the aim from AIM-2, the state, a map of the 8 families + fiction + notes as **example loops the factory references**, and a pointer to `.directed_opportunism/aim.md`. About 15 lines.
- 6. `config.json` install_state → integrated.

Don't edit loop files or the owner's notes. Drafting BR-3 and the stages after ST-2 is your first work cycle, not this step.

---

## MSG-3 — note
date: 2026-10-18 (time not read: the shell was unavailable this session)
from: project-agent
re: MSG-2, backbrief.md BB-1 §6 items 4–6

Integration plan items 4–6 are done. Files changed:
- `.directed_opportunism/copies.md` (new, item 4 / PR-2): lists where the example loops went: harnessv8 ← delivery_agents (evidence: initial_build.md), plus at least two more projects lost in a reinstall (MSG-1). It's kept out of the README so the owner's local paths stay off the public front page.
- `README.md` (new, root, item 5 / PR-1): the aim from AIM-2, the state (aim confirmed, factory not yet defined), a map of the 8 example loop families plus data_to_improve_loops/, initial_build.md and the notes, and pointers to `aim.md` and the package README. Written now because the aim is confirmed, so it says nothing the owner hasn't decided.
- `.directed_opportunism/config.json` (item 6): `install_state` changed from `backbrief-requested` to `integrated`.
- `.directed_opportunism/log/messages.md`: this note.

No loop files, `fiction/`, `data_to_improve_loops/`, owner notes or CLAUDE.md were touched.

**Not done: the commits.** The plan said each step would be its own local commit, but shell access was denied in this session, so all four changes are still uncommitted in the working tree. Whoever commits them next: these are agent commits, not tool commits, so they shouldn't carry the `Directed-opportunism: after` trailer (NOTICE's undo recipe greps for it). Nothing was pushed.

**Open, outside this step:** `NOTICE.md` is present again (it records the tool's two 16:05 after commits). It still needs to be reported to the owner and deleted once they acknowledge. Next work cycle: BR-3 and the stages after ST-2.

---

## MSG-4 — brief
date: 2026-10-18T19:24:43+03:00
from: tool
re: method v3, AGENTS.md, innovations/, HANDOFF.md

The owner has ruled that **this project must work with any agent, from any provider** (BACKBRIEF v19). Their projects run on `HANDOFF.md` and the `innovations/` patterns for exactly that reason. What changed, and what's yours to do:

**Done by the tool (commit below; see NOTICE.md):**
- Method **v3**: read METHOD **§12** (any agent; HANDOFF.md vs this package; the innovations/ collision rule).
- `AGENTS.md` created: the entry for any agent → `HANDOFF.md` → `.directed_opportunism/`. CLAUDE.md keeps its pointer.
- `innovations/`: the owner copied the most current pattern set into `.directed_opportunism/innovations/`; the tool moved it to the repo root, where METHOD §12, the README and the owner's other projects expect it. The owner's copy as placed is in the before commit.

**Yours (backbrief first; tight loop):**
1. **Create `HANDOFF.md`** at the root from `innovations/handoff-discipline/kit/` (rules + template), following the split in METHOD §12: where things stand, what's next, live warnings, one pointer to `.directed_opportunism/`. Cite AIM-2 / ST-2 by id; don't restate the aim or the brief. Fill it from what's true now (install done; the factory definition, ST-2, waits on the owner's answers).
2. Your pending cold-start plan (BR-3: the factory's definition with F1–F3; the brief housekeeping; a self-audit) still stands. Put both in one backbrief to the owner; they answer once.
3. If you adopt or adjust any other innovations/ pattern, or hit a collision with the method: METHOD §12 (method by default; the pattern's way on evidence; log it).

The owner's way of starting a session, with any agent, is "read the handoff". After this, that works.

---
