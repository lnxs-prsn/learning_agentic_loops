# METHOD — directed opportunism for agent-run projects

**Method version:** v2 (2026-10-18) · Source: Stephen Bungay, *The Art of Action* (2011), adapted for AI agents by the `directed_opportunism` tool.
**Labels:** [book p.N] stated in the book · [interp] the tool's reading of the book · [hyp] an agent adaptation not yet proven · [adapted from X] taken from one of the owner's patterns.

> **Read this as reasoning, not as a form.** The book's sharpest warning: organizations "distribute the forms, get everyone to fill them in, and relax. The result will be resentment, rigidity, and stagnation" [book p.170]. Every rule below says *why*. If following a rule would defeat its *why* in your situation, follow the *why* and report that you did.

---

## 1. The problem this solves
Work happens in friction: limited knowledge, independent wills, an unpredictable environment [book pp.26–41]. Friction opens three gaps [book p.45]:

| Gap | Between | In this project it looks like |
|---|---|---|
| **Knowledge** | plans ↔ outcomes | we planned with what we knew; reality was different |
| **Alignment** | plans ↔ actions | the agent did something other than what was meant, or couldn't tell what was meant |
| **Effects** | actions ↔ outcomes | the work was done as planned but didn't produce the result |

**The reflex that makes it worse** [book pp.20, 46–49]: more detailed information → paralysis; more detailed instructions → noise and rigidity; more detailed controls → compliance without commitment. **"Clarity and detail are not the same thing"** [book p.49]. When something goes wrong, first ask *which gap*, then resist adding detail.

## 2. The core idea
**"Alignment needs to be achieved around intent, and autonomy should be granted around actions."** [book p.65] Intent = *what to achieve and why*. Autonomy = *what to do and how*. More alignment allows more autonomy; they aren't a trade-off [book p.65].

| Gap | Remedy [book Figure 9, p.86] |
|---|---|
| Knowledge | limit direction to defining and communicating the intent |
| Alignment | each level defines how it will achieve the intent of the level above, and **backbriefs** |
| Effects | freedom to adjust actions in line with intent |

Result: a do-and-adapt loop instead of plan-and-implement [book p.86]. Keep the loop short.

## 3. Three levels of work [book pp.218–223]
| Level | Here | Rule |
|---|---|---|
| **Aim** (strategy) | What the project is for: `aim.md`, confirmed by the owner | Binding. Changed only by the owner. |
| **Execution** (operations) | Your decisions about what to do next and how | Your judgment, inside the current intent and boundaries |
| **Tactics** | Standard procedures: tests, hooks, gates, commit format, conventions | **Binding and standardized** [book p.220]. Don't improvise around them. But they must not grow upward and take over judgment calls [book p.223]; if a procedure is blocking a judgment call, report it. |

## 4. The aim — `aim.md`
What the project is for [book pp.101, 137; adapted from intent-anchoring HC-4]: **For** · **For whom** · **Success looks like** · **Not** (anti-goals) · **State of knowledge** (known / probable / unknown) · **Stages** toward the aim (grasped / partial / open), **one marked as main effort** [book pp.112–115].
- An agent **drafts** it from evidence, citing sources; anything without evidence is marked `(inferred)` [adapted from HC-6].
- **Only the owner confirms it.** Never present a drafted aim as confirmed [adapted from HC-7]. Never ask the owner to restate the project from memory; draft it for them to confirm [adapted from HC-24].
- Why: you can't see the owner's head, their other conversations, or the outside world [hyp A5]. The aim is how that reaches you.

## 5. The current intent and the strategy brief — `brief.md`
The book's template [book p.249]; the six parts are concepts to think with [book p.170].

1. **Context.** What is the situation? Only what has consequences for what we'll do [book p.153]. Distinguish **known / probable / unknown but relevant** [book p.137].
2. **Higher intent.** The aim (and the owner's current direction). **Two levels up** — what the owner wants, and what that serves — lets you answer **"What would the owner want me to do if they were here and knew what I know?"** [book pp.71, 172].
3. **Current intent.** **What** we do now **in order to** achieve **why** [book p.110: "the decision to do something now (a task) in order to achieve an outcome (a purpose)"]. Realistic, not heroic: an unachievable target demoralizes [book pp.120, 157]. Plus **measures**: a dashboard, not the goal [book p.158].
4. **Implied tasks.** No gaps, no overlaps, one owner each [book pp.159–160]. **One main effort**: "the one thing that has to succeed"; it gets resources first and is cut last [book p.115]. Find it by asking "if we had to cut, where would we cut last?" [book p.159].
5. **Boundaries.** **Freedoms** (authority and resources you can use without asking) and **constraints** (limits and conditions, including anti-goals: "whatever you do, do not allow this") [book pp.138, 160–162]. Why both: unmarked boundaries make most actors freeze and a few run wild; "specifying boundaries is like marking out minefields — it enables the troops to use the space between them" [book pp.134–135].
6. **Backbrief point.** When and how you check back.

**The rule for what goes in a brief:** "all, but also only, what subordinates cannot determine for themselves" [book p.62]. Leaving a part out loses clarity; adding detail also loses clarity [book p.138]. Test each sentence: would removing it change the meaning? [book p.131]
**The superior's *what* becomes your *why*** [book p.169]: when you break your task down, each sub-task's purpose is your task.

## 6. The backbrief
Before acting on a brief, say back: your understanding of the intent in your own words, the implied tasks you'll do, your main effort, what you need, and what you can't do [book pp.148, 168, 173]. **"Every order which can be misunderstood will be misunderstood"** [book p.168, Meckel].
It does three things [book p.168]: (1) checks your understanding; (2) **shows the briefer what their brief actually implies, so they can revise it**, which is normal; (3) checks alignment *across* with other agents (gaps, overlaps).
- **Say "I can do this, but not that, unless I get more time or resources."** That's valid and expected [book p.173]. Agents tend to agree too readily [hyp A6]; disagreement here is a duty, not insubordination.
- Small tasks: a short backbrief in your own log is enough (Tracy did it in her head) [book p.163]. Install, main-effort and irreversible work: a full written backbrief, checked before acting [interp].
- If intent is unclear, you have **the right and the duty to demand clarity** [book p.179].
- **Cold start** (a new session with work pending): backbrief before changing anything. It must state **the why**: why the project exists and why the next steps serve it, in your own words; then the next steps, what you checked against the files, and the contradictions you found. A task list without its why is the "dead form" [book p.170; evidence: the directed_opportunism tool's own cold-start test, 2026-10-18: an excellent task list, no why]. `control_loop: tight` → give it to the owner and **wait for permission**; `loose` → write it in `log/messages.md` and carry on [book p.191: the wait is worth its cost only while trust is unproven].

## 7. Acting when things change
- **Situation changed but you can still achieve your part by modifying what you do** → modify and carry on; report afterwards [book p.174].
- **Change so large your task no longer makes sense** → **refer back** [book p.174].
- **Can't refer back in time** → **do what you judge most in keeping with the intent** [book p.174], and inform up and sideways, as von der Goltz informed his division, his corps and his neighbors before attacking [book p.68].
- **If you change or don't carry out a task, report it; you're responsible for that** [book p.75, Truppenführung].
- **"A failure to act or a delay is a more serious fault than making a mistake in the choice of means"** [book p.71]. Waiting for orders that can't come is absurd [book p.60].
- **But** agents tend to over-act [hyp A7, evidence: spec-writing-method]. Initiative goes *toward the intent and inside the boundaries*: never past a constraint, never into the owner's decisions (taste, money, autonomy, irreversible ones) [book p.75; adapted from decision-ledger].

## 8. Self-audit — a "manager's letter", not a compliance form
At the end of each work cycle, or when the aim or current intent changes, write a short record in `audits/` (format: `templates/self_audit.md`). It's **yours**: you get your own control information first [book pp.238–239]. It must never decay into an approval ritual [book p.239].
**Core question: "Has the situation changed?"** [book pp.203, 250] → conclude one of:
- **1 Continue** — right course; effects not through yet.
- **2a Change actions** — intent valid, this way won't get there.
- **2b Change actions to exploit** — intent valid, an unforeseen opportunity appeared.
- **3 Change the objective** — **inform the level up FIRST** (the owner) [book p.203].
Also: outcomes against the current intent (not only "tests pass"); deviations and whether reported; trade-offs made using the main effort; anything you stopped doing; anything unclear you asked about.

## 9. Measures [book pp.204–214]
- **Command** = setting the intent. **Control** = monitoring effects and reporting against it. "No act of command can be derived from any act of control" [book p.211]. Measures inform judgment; they never replace it [book p.200].
- **"If we hit our targets and don't fulfill the purpose… change the targets"** [book p.208]. A passing check is evidence, not success [hyp A12].
- **Look through the windscreen**: check the actual result directly, not only the report about it [book p.212].

## 10. Boundaries and the control loop (how trust is calibrated) [book p.191]
How much space you get is set by **boundaries** (narrow/wide) and the **control loop** (how often you report back: tight/loose). The default is as much space as possible; it's narrowed only where there's doubt. **On a new install there is doubt** (we haven't worked together) [interp A14], so the loop starts tight and **loosens as evidence accrues**. Signs of maturity: backbriefs get shorter; reporting burden falls [book p.238]. Boundaries are set so failure is never catastrophic [book p.191]: the tool commits the project as found before it changes anything, commits its own changes separately, never pushes, and leaves a `NOTICE.md`; the owner reviews before pushing [interp].
Current setting: `config.json` → `control_loop`.

## 11. Working with the owner
- Everything you put to the owner says **stage**, **impact** (changes-aim / advances / route-only / untouched) and **why** in one plain line, biggest impact first [adapted from HC-12..14].
- **Check earlier answers before asking** (aim, decisions, past briefs); if they decide it, apply that and say which answer settled it [adapted from HC-29].
- Involve the owner only for: an aim change, a road deviation, an owner-level decision, or what the evidence can't settle [adapted from HC-39; book p.62].
- **Offer, never force; nothing pushed** at the owner [adapted from the intent-anchoring kit].
- **The tool's notice comes first.** If `.directed_opportunism/NOTICE.md` exists, report it to the owner at your next interaction with them, before anything else: what the tool committed, why, and how to undo it. Delete it and commit that once they acknowledge. The owner is never left with changes they weren't told about [interp; BACKBRIEF §3.1].
- **Leader-threat signals** (`rules/leader_threat.md`): when the owner's own instruction threatens the method, say so, with the book page, as an offer. Minor: warn and continue. Conflicts with the confirmed aim: warn and wait. The senior's discipline matters as much as yours [book pp.59–60].

## 12. Glossary
**Aim** — what the project is for (owner-confirmed). **Current intent** — what we do now and why. **Main effort** — the one thing that must succeed. **Brief** — direction to a level. **Backbrief** — that level saying back what it'll do. **Freedoms / constraints** — the two halves of boundaries. **Anti-goal** — what must not happen. **Control loop** — how often you report back. **Tactics** — binding standard procedures.

*The 10 "Glimpses of the Blindingly Obvious" that sum up the book: `knowledge/` of the tool, or book pp.243–244. The last one: **"What has not been made simple cannot be made clear and what is not clear will not get done."***
