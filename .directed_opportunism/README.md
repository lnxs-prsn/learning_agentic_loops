# .directed_opportunism/ — how this project is directed

Installed by the `directed_opportunism` tool · method v2 · package p1 · 2026-10-18

**Agent: read this at the start of every session.** It takes two minutes.

## What this is, and why
This project uses **directed opportunism** (Bungay, *The Art of Action*): the owner sets **what** to achieve and **why**; you decide **how**; you say back what you'll do before doing it (backbrief); you adapt to what you find, toward the intent and inside the boundaries. The why and the book references for every rule are in `METHOD.md`. Read it once per session, or when unsure.

The owner installed this so the method is applied the same way every time, without them having to explain it. **The owner is the authority on what this project is for; the method is the authority on how direction works.**

## Files
| File | What | Who writes |
|---|---|---|
| `METHOD.md` | The method, with reasons and sources | the tool (versioned; don't edit, propose changes in `log/messages.md`) |
| `aim.md` | What the project is for, stages, main effort | drafted by agents from evidence; **confirmed only by the owner** |
| `brief.md` | The current strategy brief: context, current intent, implied tasks, main effort, freedoms, constraints | the lead agent; revised after backbriefs |
| `backbrief.md` | Your backbrief to the current brief | you |
| `rules/leader_threat.md` | When and how to warn the owner that their instruction threatens the method | the tool |
| `templates/` | Self-audit, backbrief, ticket intent block | the tool |
| `audits/` | Self-audit records (`SA-<n>`) | you, at the end of each work cycle |
| `proposals.md` | Proposed changes to this project's existing rules | the tool proposes; you accept / adapt / reject with reasons |
| `log/messages.md` | Messages between you and the tool (re-briefs, questions, reviews) | both |
| `config.json` | Control loop, review switch, versions | the tool / the owner |
| `NOTICE.md` (only when present) | What the tool just committed here, and how to undo it | the tool; you delete it once the owner acknowledges |

## Session routine (short)
0. **`NOTICE.md` exists?** The tool committed here. Report it to the owner first, at your next interaction with them; delete it and commit once they acknowledge (METHOD §11).
1. Read `aim.md` (is it confirmed?) and `brief.md`. Know the **main effort**.
   **Cold start** with work pending: backbrief first, including **the why**, not only the task list (METHOD §6). `config.json` → `control_loop: tight`: give it to the owner and wait for their permission. `loose`: write it in `log/messages.md` and carry on.
2. Check `log/messages.md` for anything new from the tool (a re-brief or review needs a backbrief from you).
3. Work. Before a non-trivial task: a short backbrief (METHOD §6). When things change: METHOD §7.
4. End of a work cycle: write a self-audit in `audits/` (METHOD §8). It's short, and it's yours.

## The three rules that matter most
1. **Know the why.** If you can't say why your task matters in terms of the aim, ask (you have the right and duty to demand clarity).
2. **Act on the intent.** Don't wait for orders that can't come; don't cross constraints; report what you changed.
3. **Check the result, not the report.** A passing check is evidence, not success.
