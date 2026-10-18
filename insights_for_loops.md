insight 1 
"
# Report: Ecosystem and Plan-as-Continuous-Process, Applied to Agentic Loops

## 1. The two source ideas

**Idea A, war origin: the opponent is not the fundamental unit of analysis.** The unit is the coupled system of you plus your environment (the "small patch of woods"), and the opponent is one parameter within it. Success means staying viable, not defeating a counterpart.

**Idea B, plan origin: planning never stops, and execution is part of planning.**
- **Small executions, replanned often.** The overall plan can be huge, like building a space station.
- **Execution is data.** It feeds the next small plan and is not a separate phase.
- **The framework** responds to reality as it is now and produces a **now-plan**. It feeds that back to the **segment plan**. It runs in and between seams, and it can replan drastically if needed. No simulation of the future is required.
- **Seams** are where a segment ends and a commitment is made.
- **The success clause**, usually called failure: if the now-plan drifts too far from the segment plan, planning can cheaply conclude the goal is unreachable.
- **Segment size is designable.** A large segment can contain its own checkpoints.

## 2. What each supplies, and what each lacks

| | Supplies | Lacks |
|---|---|---|
| **A: ecosystem** | The right thing to measure: system viability, not task completion. Shared state as coordination, so nothing has to route through a single parent. A rule for recursion: spawn a new regulator when the environment's variety exceeds what existing loops handle. | When to change course, how to change it, and when to stop. |
| **B: plan** | A change process (the framework and seams). An honest, cheap exit (the success clause). Cheap failure through small segments. | A reason to look beyond the plan. On its own it is task-shaped, closer to subagents with better feedback. |

A says what matters, and B says how to adapt and when to quit.

## 3. The combination in agentic-loop terms

| Element | In loop terms |
|---|---|
| Viability (A) | Each loop is judged on the health of the shared state it regulates, not only on task return values |
| Now-plan (B) | Each loop continually re-derives "the best plan from here" from current reality |
| Segment plan (B) | The intended plan for this stretch of work, fixed until a seam |
| Distance | Gap between now-plan and segment plan, the drift signal |
| Checkpoint | Save point inside a large segment, with no authority to change the plan |
| Seam | The meta-loop's decision point: continue, retune, replan drastically, spawn or retire a loop, or invoke the success clause |
| Success clause | Pre-declared, numeric condition under which the goal is declared unreachable by planning |
| Requisite variety (A) | The trigger for spawning a new loop |
| Segments containing segments | Loops that build loops, recursively |

**One-line version:** loops regulate viability of shared state, replan continuously from reality, commit at seams, and stop honestly when the now-plan drifts too far from what the goal requires.

## 4. Sketch of the loop spec

```python
@dataclass
class LoopSpec:
    observes: list[str]          # environment slice it senses
    acts_on: list[str]           # what it may change
    segment_plan: Plan           # intended plan for this segment
    replan: Callable             # reality -> now-plan
    distance: Callable           # now-plan vs segment plan
    checkpoint_every: Trigger    # save state, no authority
    seam_policy: SeamPolicy      # continue | retune | replan | spawn | retire
    unreachable_when: Callable   # pre-declared, numeric
    budget: Budget               # depth, count, cost, time
```

## 5. Where it helps

- **Local success hiding system damage.** Viability signals catch what "task returned success" misses.
- **Endless retrying.** The success clause gives agents an honest exit, which most stacks lack.
- **Cost.** With no simulator, drift is the distance between two plans, which is cheap to measure.
- **Long-running, changing work.** There is no fixed "done," so continuous replanning fits better than one-shot delegation.
- **Parent bottleneck.** Coordination through shared state removes the need for one context window to understand everything.
- **Runaway spawning and oscillation.** Seams and budgets bound when and how loops change.

## 6. Where it hurts

- **Overkill for bounded tasks.** For "fix this bug," subagents are simpler, cheaper, and easier to trace.
- **Distance is ambiguous.** A large gap can mean a big detour that is still feasible, or a goal that is out of reach. I suggested separating structural distance (how much the plan changed, which sets the level of rework) from feasibility gap (now-plan cost against remaining budget, which sets "unreachable"). You haven't chosen yet, so this is my proposal and not part of your idea.
- **Planner noise.** An LLM producing the now-plan may give different plans from the same state, so distance could reflect variance and not reality. Tolerance bands or repeated planning would help.
- **Slow drift.** Small gaps under the threshold can accumulate, so track cumulative distance and rebase at seams.
- **The stop clause.** It must be numeric and pre-declared, or a model can game it by quitting early or never quitting.
- **Debuggability.** Coordination through shared state is harder to trace than a call stack, so log environment state and every now-plan.
- **Reversibility.** Checkpoints only make failure cheap if state can be restored, so place them before irreversible actions.

## 7. Prior art

- **Kubernetes controllers** are reconciliation loops chained through shared state.
- **Erlang/OTP supervision trees** are recursive viability maintenance.
- **Blackboard architectures** and **stigmergy** coordinate through a shared workspace.
- **Beer's Viable System Model** is the theory behind the recursion.
- **Plan repair and plan stability** in AI planning is the closest match for the now-plan versus segment-plan comparison. I'm not aware of anyone using the distance itself as the stop signal, but I haven't searched for it.

None of these is LLM-driven, so how this behaves with probabilistic, costly agents is unproven.

## 8. A cheap judgment layer

Many decisions here are frequent and narrow: is the distance over the threshold, is this data noise, should a seam fire. A cheap decision model (such as Jev, discussed earlier) could answer these as typed questions, and the frontier model would only produce the now-plan and drastic replans. That is a cost optimization and does not change the design. Independent evidence on its reliability is still thin.

## 9. Verdict

- **Beneficial** for long-running, changing, or open-ended systems, and wherever local task success can hide global degradation.
- **Unnecessary** for bounded, short, traceable tasks.
- **Best likely design is a hybrid:** subagents for tasks, loops for maintaining conditions, and a meta-loop that decides which to use.
- **The combination beats either idea alone.** A gives the unit of analysis, and B gives the operating discipline and the exit. Neither is proven to beat subagents in general.

## 10. How to test it

Build a subagent version and a loop version of one non-trivial system and compare:
1. Failure recovery (inject a failure, measure time and appropriateness)
2. Long-run drift in system quality
3. Cost per unit of useful work
4. Human debug time
5. Stability (oscillation, spawn counts)
6. **Which layer caught each failure** (checkpoint, seam, or success clause)

If sub-loops win on 1 and 2 but lose on 3 to 5, the honest conclusion is "worth it only for long-running systems."

## 11. Open decisions

1. **What counts as distance?** Steps changed, cost to goal, or both?
2. **What ends a segment?** A step or time limit, a distance threshold, or a state change in the situation?
3. **What can a checkpoint do?** Only save and flag, or force an early seam when a threshold is crossed?

The first is the most urgent, since the success clause depends on it.
"


insight 2
"
# Does "ecosystem over opponent" improve agentic loop design?

**Verdict:** partly. The idea is a useful design lens for a narrow class of systems, but it isn't a general replacement for subagent orchestration. It is also less novel than it feels, which is good news because it means there is prior art to learn from.

## 1. The idea without the war

In war terms, the claim was that the opponent isn't the fundamental unit of analysis. The unit is the coupled system of you plus your environment, and the opponent is one parameter in it. For agents, that becomes:

- **Subagent design:** the unit is the *task*. A parent decomposes, delegates, and collects results, and success means the task is done.
- **Sub-loop design:** the unit is the *viability of the whole system*. Loops regulate conditions in shared state, and success means the system stays healthy over time.

## 2. Where it helps

- **Goal completion vs. system health.** Subagent systems optimize "task returned success." An agent can pass its tests while degrading the codebase, or finish a scrape while corrupting the data store. This is the Pyrrhic-victory problem: winning the local task while losing the wider system. A viability signal catches what a completion signal can't.
- **Long-running, open-ended work.** Monitoring, maintenance, research that never ends, and systems whose environment keeps changing. Here "done" doesn't exist, and regulation is the right frame.
- **Removing the parent bottleneck.** A parent that must understand every subtask becomes the limit on system capability. Loops that coordinate through shared state don't route everything through one context window.
- **Recursion with a rule.** Ashby's law of requisite variety says to spawn a new regulator when the environment's variety exceeds what existing loops can handle. That is a principled trigger, whereas most spawning today is ad hoc.

## 3. Where it fails or costs more

- **In war you can't choose your environment. In software you can.** Most agent work is bounded ("fix this bug," "write this report"), and for that call/return is simpler, cheaper, and far easier to debug. Ecosystem framing adds machinery to problems that don't need it.
- **The adaptive-adversary problem returns inside your own system.** Loops that adapt to each other can oscillate, fight over the same variables, or drift into behavior nobody designed. The wolf you're worried about is now your own loop.
- **Viability must be measurable.** If a loop's health signal is vague, the meta-loop has nothing to steer by, and LLM-judged "health" is noisy and gameable. Without observable signals, the design collapses into unstructured agent chatter.
- **Cost and runaway risk.** Persistent loops burn tokens continuously, and loops that spawn loops need hard caps on depth, count, and spend.
- **Debuggability.** A call stack is traceable, but emergent coordination through shared state is not. You would need full environment-state logging, and replaying failures is much harder.

## 4. The idea is already proven outside LLM agents

This is the most important finding. Several mature systems work this way:

- **Kubernetes controllers** are reconciliation loops. Each observes state, acts, and converges toward a desired condition, and one controller's output (a new resource) becomes another controller's input. That is sub-loops through shared state, running in production at scale.
- **Erlang/OTP supervision trees** are recursive: supervisors restart failing processes according to policy, which is "loops that maintain viability of loops."
- **Blackboard architectures** (Hearsay-II is the classic) coordinate independent specialists via a shared workspace, and **stigmergy** does the same in swarm systems.
- **Beer's Viable System Model** is the theoretical version of the same recursion.

So the idea is real and well-tested for infrastructure. What is unproven is how it behaves with LLM-driven loops, where each loop is probabilistic, expensive, and prone to reward hacking. I haven't searched the current agent literature for direct experiments, so treat that gap as "not established" rather than "confirmed absent."

## 5. Where each approach wins

| Situation | Better fit |
|---|---|
| Bounded task with a clear finish | Subagents |
| Ongoing condition to maintain | Sub-loops |
| Need strict traceability | Subagents |
| Environment changes unpredictably | Sub-loops |
| Tight cost limits | Subagents |
| Parent can't hold the full picture | Sub-loops |

The most likely good design is a hybrid: subagents for tasks, loops for maintaining conditions, and a meta-loop that decides which to use.

## 6. How to know if it's beneficial

Build both versions of one non-trivial system and compare them on:

1. **Failure recovery:** inject a failure and measure time to recovery and whether the fix was appropriate.
2. **Drift:** run for a long period and measure system quality, not just task success.
3. **Cost:** tokens and time per unit of useful work.
4. **Debug time:** how long it takes a human to explain a bad outcome.
5. **Stability:** oscillation, spawn counts, and runaway behavior.

If sub-loops win on 1 and 2 but lose on 3 to 5 for your workload, the honest conclusion is "worth it only for long-running systems."

## 7. Recommendation

- **Keep** the core insight: measure system viability, not just task completion.
- **Don't claim** it beats subagents generally. It doesn't, and the war framing overstates the contrast, just as "duel ontology" was a strawman.
- **Borrow** the tested mechanisms (reconciliation loops, supervision policies) instead of inventing coordination from scratch.
- **Start small:** one meta-loop, two child loops, hard spawn limits, and an explicit health signal per loop.

The original war-context claim survives in weaker form: the coupled system is a better unit of analysis than the individual task for some systems, and worse for others. The value of your idea is knowing which is which.

Want me to search for existing research on LLM-agent systems built this way, to see whether anyone has already tested it?
"

insight 3
"
    # Report: Two-Lever Model & Its Applications

## The Core Idea

You proposed that **moving toward failure and moving toward success are not the same axis with opposite directions — they're two independent levers.**

- One lever governs movement toward/away from **X (failure)**
- A separate lever governs movement toward/away from **Y (success)**
- They are not mirror images of each other on a single dial; they can move independently, together, or not at all

This breaks the intuitive assumption that "not failing" = "succeeding," or that reducing risk is the same move as pursuing a goal, just pointed the other way.

**The four states this produces:**

| Failure-lever | Success-lever | Result |
|---|---|---|
| Retracted | Engaged | Ideal — safe and growing |
| Engaged (moving toward X) | Engaged | Growing but accumulating risk |
| Retracted | Disengaged | Stagnant but "safe" — the zombie state |
| Engaged | Disengaged | Active collapse |

The dangerous ones are the middle two, because from the outside — or from a single dashboard — they can look identical to the ideal state if you're only watching one lever.

## Fits Found

**1. Cognitive/behavioral science precedent**
Gray's approach/avoidance framework treats reward-pursuit and punishment-avoidance as separate neural systems, not opposite ends of one motivational dial — people can score high or low on each independently. Herzberg's two-factor theory makes the same claim for job satisfaction: the things that cause dissatisfaction and the things that create motivation are different mechanisms, not opposite ends of one scale.

**2. Your own business framework (nested spaces)**
This turned out to be the same shape, already built, without you having named the mechanism yet:
- **Pure-state invariants** (safety, legality, solvency) = the failure-lever. A floor. "Never move toward X."
- **Profit** = the success-lever. An open direction. "Keep moving toward Y."
- The reason your framework kept these as *separate, non-collapsing categories* instead of one spectrum is exactly this two-lever structure — you'd already encoded the insight structurally before articulating it as a general principle.

**3. Startup failure diagnostics**
This is where the model produced a real predictive claim, not just a relabeling:
- Most startup failures are **failure-lever violations happening while the success-lever is working fine** — cash floor breached, cofounder relationship collapsed, legal exposure realized — all while growth metrics looked healthy. "We grew 20% monthly and ran out of runway" is the two-lever model's signature failure pattern.
- The inverse also exists: startups that never violate anything (cautious, compliant, cash-safe) but never engage the success-lever hard enough to find product-market fit — the "safe zombie."
- The sharper postmortem question this generates: not *"did they pursue success hard enough,"* but *"which floor went uninstrumented, and was that absence caused by all attention being spent on the success lever?"* Founder attention and dashboard/pitch-deck language cluster almost entirely on success-lever metrics (growth, TAM, traction), while the actual causes of death cluster on failure-lever categories (cash, team, timing) — a structural mismatch between where attention goes and where the real risk sits.

## What's Still Open

- A general method for **instrumenting** the failure-lever with the same rigor startups already give the success-lever (what would a "failure-lever dashboard" concretely track, beyond cash runway?)
- Whether this two-lever structure generalizes below the org level — to a single project or even a single skill you're building (e.g., is there a failure-lever/success-lever split in how you're approaching the job search or a specific project like SliceKit?)
"





insight 4
"
 # Report: Managing Irrelevant Information in Agentic Loops

## 1. Summary

An agent loop's goal stays fixed while its state changes every step. Information that was relevant at step 3 is often noise by step 15. Deciding what to add is a one-time judgment. Deciding what to remove has to be repeated every step. Without a deliberate removal policy, quality degrades silently and cost grows linearly with loop length.

**Core claim:** Knowing what is irrelevant is at least as important as knowing what is relevant, because irrelevance is what accumulates unnoticed.

## 2. Why Irrelevance Management Matters

The argument, step by step, so each link can be checked:

| # | Premise | Consequence |
|---|---------|-------------|
| P1 | Relevance is defined relative to the current step, not the whole task. | Relevant information expires as state changes. |
| P2 | Each loop step appends output (tool results, attempts, reasoning). | Context grows monotonically unless something removes it. |
| P3 | The model's attention is finite and every token competes for it. | Irrelevant tokens dilute relevant ones, so performance degrades before the hard limit. |
| P4 | Stale content (failed attempts, superseded plans) stays in context. | The model anchors on it, retries dead ends, or treats old errors as live facts. |
| P5 | Cost and latency are paid per token, per step. | Context carried for N steps costs N times. |
| P6 | Degradation from noise produces no error message. | The failure is silent, so it must be prevented by design rather than caught by exceptions. |

**Conclusion:** From P1 to P6, an add-only loop is guaranteed to get worse over time. Removal and compression are required parts of the design.

**The asymmetry:**

- Wrongly discarding something relevant is *loud and recoverable* if a pointer to the source was kept.
- Wrongly keeping irrelevant material is *silent and cumulative*.

This is why the default policy should lean toward distilling and evicting, with cheap re-fetch as the safety net.

## 3. Classification Model

Every item entering context gets a lifetime class, which determines its retention policy.

| Class | Examples | Policy |
|-------|----------|--------|
| **Permanent** | Goal, constraints, success criteria | Always in context; never evicted |
| **Task-scoped** | Current plan, key findings, decisions made | Keep in compressed form; update as the plan changes |
| **Step-scoped** | Raw tool output, file contents, search results | Distill to a conclusion after use, then evict |
| **Ruled-out** | Failed approaches, rejected hypotheses | Keep as a one-line note (what, why it failed) |
| **Noise** | On-topic but non-actionable content | Reject at admission |

## 4. The Plan

Five stages, applied every step:

1. **Admit.** Before adding an item, tag it with a class. If it fits none, or fails the test in Section 5, don't admit it.
2. **Distill.** After the item has been used, replace it with its conclusion plus a pointer (path, URL, query) so the raw data can be re-fetched.
3. **Evict.** Remove step-scoped items once distilled. Collapse completed subtasks into one-line summaries. Drop dead-end branches, leaving a ruled-out note.
4. **Externalize.** Store the archive (full logs, raw outputs, history) in files or a database. Context holds working memory only and reloads from storage on demand.
5. **Verify.** Periodically check that the compressed state still supports the next decision and that the goal is still intact.

## 5. Decision Rules

- **Relevance test:** Does this change what I do next? If not, distill or drop it.
- **Recoverability test:** Can I re-fetch it? If yes, evict aggressively. If no, keep a compressed copy.
- **Staleness test:** Has the state changed since this was recorded? If yes, re-verify or remove it.
- **Contradiction test:** Does it conflict with newer information? If yes, remove the older item, don't keep both.

## 6. Invariants (must always hold)

- The original goal and constraints are present and unmodified.
- Every distilled summary has a pointer to its source.
- Every abandoned approach has a ruled-out note.
- No two items in context contradict each other.
- Context size stays below a chosen budget, independent of step count.

## 7. Failure Modes and Detection

| Failure | Symptom | Mitigation |
|---------|---------|------------|
| Over-eviction | Agent re-fetches the same thing repeatedly | Keep better distilled summaries |
| Under-eviction | Slow drift, rising cost, repeated dead ends | Enforce the context budget |
| Lossy distillation | Later steps act on a wrong summary | Keep pointers; re-fetch when stakes are high |
| Goal drift | Agent optimizes for recent items | Re-inject the goal at fixed intervals |
| On-topic noise | Plausible but useless retrieval fills context | Apply the relevance test at admission |

## 8. How to Test the Plan

- **Context size vs. step count.** It should plateau, not grow linearly.
- **Repeated-action rate.** How often the agent retries something already ruled out.
- **Task success rate at long horizons.** Compare with and without eviction.
- **Cost per completed task.**
- **Ablation.** Remove one stage (say, ruled-out notes) and measure what breaks. That shows which stage is doing the work.

## 9. Open Questions

- What is the right context budget for this task type?
- Who decides what to distill: the agent itself, or a separate summarizer? Self-summarization is cheaper but can be biased toward its own past reasoning.
- How often should verification run: every step, or every N steps?

Want this as a file (Markdown or Word) so you can keep or share it?
"


insight 5
"
## Report: Applying "Easy-Path-as-Choice" to Agentic Loop Design

**Core translation of the idea into loop terms:**
For any segment goal, multiple valid paths usually exist. Some are cheap (fewer tokens, fewer tool calls, fewer retries), some are expensive. The idea says: *always prefer the cheap valid path — but recognize that "cheap" isn't always available, and when it isn't, that's information, not a failure.* Applied to agents, this becomes a path-selection heuristic that should run at spawn time and at every replan seam.

### 1. Where it plugs into your existing design

**At spawn time (before a sub-loop is instantiated):**
The parent loop should ask "is there a structurally simpler decomposition of this segment before I commit a sub-loop to the current one?" This is cheap to check and expensive to skip — a sub-loop that grinds through a hard decomposition when an easy equivalent existed is wasted compute, not virtue.

**At the seam (your replan point):**
Classify the friction encountered in the last segment as one of two types:
- **Intrinsic** — the problem genuinely requires that much search/iteration (e.g., no shortcut exists given current state/tools). Correct response: commit, don't waste cycles hunting for a shortcut that isn't there.
- **Extrinsic** — friction came from a bad tool choice, wrong abstraction, unnecessary coupling, or a decomposition that fought the problem's actual shape. Correct response: replan around it, possibly with a different sub-loop structure entirely.

This classification is the direct execution-layer analog of "was this hardship load-bearing or self-imposed."

**Feeding the success/failure clause:**
If a sub-loop keeps needing high-cost reps and the distance from the segment plan keeps growing anyway, that's a strong signal the friction is extrinsic and persistent — this is a cleaner, earlier trigger for your failure clause than just "distance grew too much." Distance-growth alone doesn't tell you *why*; pairing it with intrinsic/extrinsic classification tells you whether to replan the approach or conclude the goal is currently unreachable.

### 2. Concrete rule to bake into the framework

> Before continuing a segment under difficulty, ask: has the difficulty *changed my model of the problem* (new information suggesting a different decomposition), or has it only *cost more without teaching anything new*? The first is signal to replan. The second is a candidate for the failure clause, or for backing off to a cheaper path if one exists.

This gives you a lightweight test to run at every seam instead of an open-ended "was that segment hard" judgment call.

### 3. Where this could go wrong if over-applied

If the "prefer easy" heuristic is checked too cheaply (i.e., the loop convinces itself a shortcut exists without actually verifying it), you get thrashing — constant replanning in search of an easier path that doesn't exist, which is worse than just committing to the hard one. The check itself needs a cost cap: spend at most N cycles verifying "is there really an easier way" before you're obligated to commit to the current path as intrinsic.

### 4. One-line summary for your report

**Treat difficulty as diagnostic, not as proof of progress.** A loop that grinds harder without updating its model of the problem is doing self-imposed hardship; a loop that replans in response to new information about the problem's real shape is doing the "easy path is a choice, not a cop-out" principle correctly.
"



insight 6
"
# Report: The Organism Framework for Agentic Loops

## Summary
The framework affects both design and usage. Design decides what kind of organism exists. Usage decides what you feed it, where you place it, and when you stop it. Most of the value is in usage, because a well-designed loop used in the wrong way still starves or gets eaten. This is my analysis, not an established method.

## 1. The framework in brief
An organization or organism survives when it passes three tests:
1. **Income:** it meets its own needs from a flow it controls.
2. **Environment fit:** it survives the conditions and predators where it operates.
3. **Growth path:** it can grow toward the intended outcome from where it is.

At the macro level, small units that pass these tests connect into larger ones only when connection pays each unit.

## 2. Effect on design (what gets built)

**Income becomes budget architecture.** Each loop needs its own accounting of tokens, compute, and time per cycle, with a stop rule when cost exceeds value. Provider-agnostic backends are the agent form of avoiding a single creditor, since a loop running on one vendor's credits ends up serving that vendor.

**Environment becomes boundary design.** The predators are prompt injection, runaway cost, API changes, bad tool outputs, and self-feeding error loops. The design answer is validation and permission limits at every point where outside data enters, plus logging so the loop can sense its own condition.

**Growth becomes structure.** A loop should be able to take a harder job without a rewrite, by adding sub-loops, tools, or context handling. A design that only works at one scale is the OAU pattern: viable now, with no route to the intended outcome.

**Macro design becomes composition rules.** Your sub-loop idea fits directly. Each sub-loop passes the three tests alone, and a parent composes them through common interfaces (inputs, outputs, cost reporting). A sub-loop should be replaceable, so exit is cheap and failure stays local.

## 3. Effect on usage (what happens when a loop runs)

This is the part you were unsure about. The framework applies here because a running loop is the organism in its environment, and the operator is part of that environment.

**Choosing tasks (income).** Before running a loop, compare the task's value to the cycle cost. Tasks where the loop earns more than it spends are its food. Assigning tasks below that line drains it. For a personal system this means matching task size to the budget you can sustain, rather than running loops because they exist.

**Choosing where to deploy (environment).** Give a loop tasks in conditions it fits: clean inputs for a fragile loop, messy inputs only for a loop built with an immune layer. Place risky actions (writing files, spending money, sending messages) behind permissions that match the loop's proven reliability.

**Growing usage in stages (growth path).** Start with a small, low-stakes task where failure is cheap, then widen scope as the loop shows it can feed and defend itself. This is the ECSC pattern: a small seed that earned trust before anything larger was tried. Starting a new loop on a big, visible task is the Federation mistake.

**Supervision during the run.** Treat live signals as vital signs: cost per cycle, error rate, drift from the goal, and how much context is being carried. A loop that shows rising cost with falling output is starving, and one that repeats itself is sick. Your plan-origin design already contains this: the seams are checkpoints, and the success clause (concluding the goal currently can't be reached) is the runtime kill rule. Without it, a loop that can't succeed keeps spending.

**Connecting loops at run time.** Compose loops only when the connection pays. If a parent calls a sub-loop for a result the parent could produce alone, the connection costs more than it earns.

**Ending and exiting.** Retiring a loop cleanly is part of usage. A loop that cannot be stopped, replaced, or swapped for another provider has captured its operator.

## 4. Design and usage compared

| Question | Design | Usage |
|---|---|---|
| Income | Build the budget and stop rule | Match tasks to what the loop earns |
| Environment | Build validation and permissions | Deploy where the loop fits |
| Growth | Build room for sub-loops | Widen scope in stages |
| Connection | Common interfaces, easy exit | Connect only when it pays |

Design sets the loop's capacities. Usage decides whether it stays inside them.

## 5. Where the metaphor needs care
- **Predators are less alive.** Rate limits and bad data don't retaliate the way markets do, so the immune organ is about the boundary with outside inputs more than about defense against a hostile actor.
- **Loops that build loops can breed non-viable organisms.** Each new loop should earn its budget before it runs, otherwise the parent spends its income on units that never feed themselves.
- **It is a checklist, not a proven predictor.** It gives you questions to ask about each loop. Whether it improves outcomes is something you'd test by running your existing loops through it and comparing failures against the tests.

## 6. Suggested next step
Take one existing loop and answer, in writing, for each of the three tests: where its income comes from, what would eat it, and how it grows. Then check whether its real failures came from the organ that answer flagged as weakest. If they did, the framework is useful for you in practice, and the results will show which questions matter most for usage versus design.
"




insight 7
"
# Ant-Inspired Loop Design: A Working Report

## 1. Core model

An ant colony works without a planner. Each ant follows a few local rules, the environment carries the signals between ants, and selection over time decides which rules survive. A loop can be built the same way from three separate layers:

| Layer | Ant version | Loop version |
|---|---|---|
| **Agents** | Local rules, no goal representation | Narrow role, trigger, action |
| **Environment** | Pheromone, trails, nest state | Shared state: queue, board, index, specs |
| **Selection** | Differential reproduction | Eval and filter that decides what gets reused, decayed, or retired |

The "why" lives in the third layer, not in the agents. Every design decision below follows from that.

## 2. Seven primitives

**1. Signals in shared state (stigmergy)**
- Agents coordinate by writing to shared state, not by messaging each other.
- Each entry is a small record with `type`, `payload`, `strength`, `created_at`, `source`, and `last_reinforced`.
- Agents only read what their trigger matches.

**2. Decay**
- Every signal loses strength over time unless reinforced.
- Set a half-life per signal type: minutes for "in progress" claims, days for "this approach worked."
- Below a floor, the signal is archived or deleted.
- Without decay, stale state accumulates and agents act on a world that no longer exists.

**3. Reinforcement**
- When work passes the eval, strengthen the signals and strategies that led to it.
- Reinforce by evidence of success, not by usage count alone, or the loop will lock in popular but mediocre paths.

**4. Response thresholds**
- Each agent has a cheap gate: "is the signal for my task type above my threshold?"
- Vary thresholds across agents. Specialization then emerges from who fires first, without assigned roles.
- The gate must be much cheaper than the agent's real work, ideally a rule or a tiny model call.

**5. Degeneracy**
- For each important need, keep at least two different strategies that can satisfy it, such as different tools, prompts, or decompositions.
- On failure, weaken the failed strategy's signal so another one wins next time. Do not retry the same path.

**6. State-modulated behavior**
- The same agent shifts its thresholds and verbosity based on budget left, recent success rate, and age of the current run.
- This replaces prompt rewrites with a few numeric state variables.

**7. Two timescales**
- Fast: local rules firing on each cycle.
- Slow: a periodic pass (an ant's hormones) that retunes thresholds, decay rates, and strategy weights from accumulated results.

## 3. Recipe for a new loop

1. **Name the need**, and define what a successful outcome looks like as a testable check. This is your selection layer, so write it first.
2. **Define the signal types** the loop will use, with their schemas and half-lives.
3. **Write agents as trigger → action → signal-written.** Each one should fit in a sentence. If it needs a paragraph, split it.
4. **Set thresholds** for each agent, starting with deliberately different values.
5. **Add two strategies** for each critical need.
6. **Add hard limits:** a step cap, a token or cost budget, and a termination condition.
7. **Add the slow pass:** what gets reviewed, how often, and what it is allowed to change.
8. **Run it with logging** of which signals fired, which decayed, and which strategies won, before you tune anything.

## 4. Audit for an existing loop

Ask these questions, and treat each "yes" as a symptom to fix:

| Symptom | Ant principle missing | Fix |
|---|---|---|
| An orchestrator plans every step and everything stalls when it errs | No controller | Move coordination into shared state |
| Old results, specs, or plans still influence new runs | Decay | Add half-lives, or retire on a schedule |
| A failed step halts the pipeline | Degeneracy | Add an alternate strategy and reroute |
| Agents get long instructions covering many situations | Local rules | Split into narrow triggers |
| The loop repeats the same failing approach | Reinforcement | Weaken failed strategy signals |
| Every agent fires every cycle | Thresholds | Add cheap gates |
| Behavior is identical at 5% and 95% of budget | State modulation | Feed budget and success rate into thresholds |
| The loop drifts or invents goals | Selection outside agents | Tighten the eval and add hard limits |
| Tuning happens only when you notice a problem | Two timescales | Schedule the slow pass |

## 5. How this connects to your existing designs

Several of your own ideas already map onto these primitives, which suggests they belong together.

- **Sub-loops instead of subagents.** A colony recruits more workers when pressure in shared state crosses a threshold. A sub-loop can work the same way: spawn one when a signal type stays above threshold, give it its own budget and termination clause, and let it write results back as signals. The parent never manages it directly.
- **Plan origin (small executions, seams, replanning).** Execution results are signals that feed the next small plan. Seams are your slow-pass checkpoints. Your success clause, "the goal currently cannot be achieved," maps to the trail going cold: reinforcement stops, decay wins, and the loop concludes cheaply that the goal is unreachable.
- **Need as the gap between spirit and current state.** In ant terms, the need is the stimulus intensity. A larger gap means a stronger signal, which crosses more agents' thresholds. This gives you a concrete way to turn "need" into a number that triggers action.
- **Heuristic stack and personas.** Your usage-frequency-weighted access is reinforcement plus decay applied to heuristics. Frequently and successfully used heuristics stay strong and easy to reach, and unused ones fade. Persona capacity limits act like thresholds: a persona only fires when the signal matches its narrow set.
- **Single-cycle specs and early retirement.** This is decay applied to infrastructure and goals, so you already do it at the spec level.
- **Contracts as a hard stop.** This is where you go beyond ants. Ants tolerate messy signals because the colony is redundant. LLM agents are not, so your contracts belong at the boundary of shared state: every signal type gets a schema, and an unschema'd write is rejected.
- **Cheap daily test plus weekly reflection.** These are the fast and slow timescales from primitive 7. The daily test is the local rule, and the weekly pass is the hormonal retune.
- **Human as executive.** Until the loop has its own executive faculty, you are part of the selection layer. Log which of your judgments would need to become eval checks for the loop to run without you.

## 6. Where ant design fails for LLM agents

- **Goal drift.** An ant cannot invent a mission, but an LLM can. Keep agent prompts narrow and enforce budgets, step caps, and termination checks outside the agent.
- **Cost.** Ants are nearly free, so colonies rely on huge numbers. With expensive calls, use a handful of agents, and make threshold gates cheap so most cycles cost almost nothing.
- **Weak selection.** Ant rules were tuned over millions of years. Yours are tuned in days, so a poor eval will reliably produce agents that are good at the wrong thing. Spend the most design effort here.
- **Runaway reinforcement.** Positive feedback can lock in an early winner. Keep a small exploration rate and keep degenerate strategies alive even when one is winning.
- **Noisy shared state.** Without schemas and decay, the environment becomes a junk pile. Contracts and half-lives prevent this.

## 7. First experiments

Run these in order on one existing loop:

1. **Add decay** to one signal type and watch whether stale state stops influencing runs.
2. **Add a second strategy** for your most failure-prone step, with failure weakening the first strategy's signal.
3. **Add cheap threshold gates** to two agents and compare cost and output quality.
4. **Log everything** for a week, then run your first slow pass and adjust half-lives and thresholds from the log.
5. **Try one sub-loop spawn** triggered by a signal threshold instead of an explicit call.

## One-line principle

Agents carry no "why," shared state carries the signals, and the selection loop supplies the purpose from outside.

If you tell me which loop to start with, I can turn this into a concrete signal schema, threshold table, and slow-pass checklist for it.


"


insight 8