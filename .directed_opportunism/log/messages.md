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
5. : the owner doesn't recall its origin.
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
