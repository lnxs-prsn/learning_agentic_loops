# Aim — learning_agentic_loops

What the project is for. METHOD §4. Field names compatible with the intent-anchoring kit (adapted from HC-4/HC-9).
**Status rule:** an agent drafts from evidence (`status: derived`); only the owner confirms (`status: confirmed`, with date). Never present a derived aim as confirmed. Append new versions; never rewrite a confirmed one; mark the old one `superseded_by`.

---

## AIM-1 — (open) what learning_agentic_loops is for
status: superseded
confirmed: none
describes: 2026-10-18
evidence: folder tree (planning/delivery/debug/architecture/greenfield/migration/refactor agents, fiction/); delivery_agents/runner.md; planning_agents/16_loop_health.md; initial_build.md; fiction_build_spec.md; insights_for_loops.md (owner's notes, untracked until the install's before commit ff3c978); data_to_improve_loops/planning_agents (a smaller copy of planning_agents/, see below); one commit (71c9b34, 2026-07-11); .git/config (origin = github.com:lnxs-prsn/learning_agentic_loops); owner, 2026-10-18: "not fully planned", "in hiatus", "its loops have been used by other projects (copied)", "no clear direction"
supersedes: none
superseded_by: AIM-2
revised: 2026-10-18 by the project agent in the install backbrief (BB-1): corrected the loop count, the reading of data_to_improve_loops/, and the evidence on copies; added C3b. Still `derived`.

**The owner has no settled direction for this project (owner, 2026-10-18), so this aim is not derived as one answer: below are candidate aims for the owner to pick or correct. Nothing is built toward any of them until one is confirmed.**

### Candidate aims (the owner picks one, or corrects)
- **C1 — A library of agentic loops that other projects copy.** For: well-defined multi-agent loops (planning, delivery, debug, architecture, greenfield, migration, refactor, fiction), each with its roles and state files, ready to copy into a project. For whom: the owner's other projects. Success: a project can pick a loop, copy it, and run it without redesigning it. Not: a framework or package that projects import; not tied to one project. Evidence: the `*_agents/` folders; runner.md ("thin router"); "used by other projects (copied)" (owner).
- **C2 — A lab for improving loop design from evidence.** For: test ideas about loop design (ecosystem over opponent, plan as continuous process, irrelevance management, the organism framework) against data from real runs, and feed what works back into the loops. For whom: the owner, and through them the projects that copy the loops. Success: a design idea is accepted or dropped on evidence from a real run. Not: writing more loops for their own sake. Evidence: insights_for_loops.md (sections "How to test it", "Open decisions", "Verdict"; insights 6 and 7 each end with "run this on one existing loop"); data_to_improve_loops/ (a kept copy of the planning loop; the folder name says it is material for improving loops).
- **C3 — C1 now, C2 as the next stage** (inferred): keep the library usable as the main effort, and run design ideas as experiments against it. Evidence: both of the above exist side by side.
- **C3b — C2 now, C1 kept usable** (inferred, added in BB-1): the experiments are the main effort; the library is the test bed and is kept copyable but not extended. Evidence: the newest material in the folder is the design notes (insights_for_loops.md was never committed, so it postdates or was kept out of 71c9b34), not new loops; the notes repeatedly name "one existing loop" as the next experiment.
- (Not proposed, but possible: archive the project and leave the copies where they live. Evidence: hiatus. Listed so the choice is explicit.)

**State of knowledge**
- Known: **eight** loop families as role prompt files (planning 18, delivery 16, architecture 10, greenfield 10, debug 9, refactor 9, migration 8, fiction 5 agents + core/state/cards templates); a runner/boss/worker/reviewer/story-stage pattern repeats across them; the planning loop already has its own health dashboard (planning_agents/16_loop_health.md: convergence, feature health, spec size, cascade risk); fiction/ is an unfilled template (state files hold `"[ ]"` placeholders, chapter_count 0); **initial_build.md is a delivery spec for another of the owner's projects: every proof test runs in `/home/mr/Desktop/python/harness_design/harnessv8`**, so harnessv8 is one known consumer; insights_for_loops.md holds 7 design reports and an empty "insight 8" heading (work in progress; insight 3 strays outside loops, into startups and the owner's job search); no README, no tests, no handoff; one commit; the repo tracks a GitHub remote.
- Known (correcting the first draft): data_to_improve_loops/planning_agents is **not** a revised, larger copy. It is a *subset* of planning_agents/: no 16_loop_health.md; 00_runner 383 lines vs 576 (the main runner adds the issue log, contracts registry and loop-health calls); 07, 09, 11, 12 shorter; the other 12 files have identical line counts.
- Probable: data_to_improve_loops/ is the earlier planning loop kept as a baseline — the version that was run, and whose results drove the additions now in planning_agents/ (inferred from the folder name and the one-way difference; with one commit there is no history to confirm direction).
- Unknown but relevant: which projects besides harnessv8 copied which loops, and how they fared; whether the copies have since diverged (improvements made there and not brought back); which of C1–C3b the owner wants; whether insights_for_loops.md was kept out of git on purpose.

### Stages toward the aim (the staircase)
main_effort: ST-1

#### ST-1 — settle the direction
order: 1
contributes: everything else depends on which aim this is
state: open
alternatives: C1, C2, C3, C3b, archive
evidence: owner, 2026-10-18 ("no clear direction")

(Further stages are drafted once an aim is confirmed: the stages differ per candidate. Likely first stage after ST-1, per candidate, so the choice is concrete: C1 → list where each loop went and what changed in the copies; C2/C3b → run one experiment the notes already specify (insight 6 "three tests" on one loop, or insight 7's experiment 1, decay on one signal type) against one loop; C3 → both, library first; archive → a README that says so and where the copies live.)

**Only the owner can settle:** which candidate (or a correction); which projects copied which loops; whether insights_for_loops.md belongs in the (GitHub-tracked) repo.

---

## AIM-2 — a factory for building agentic loops
status: confirmed
confirmed: 2026-10-18, owner (at the install sitting; their words quoted below)
describes: 2026-10-18
evidence: owner, 2026-10-18; the loop families in this repo; insights_for_loops.md
supersedes: AIM-1 (candidates C1–C3b and archive: the owner chose none of them as written)
superseded_by: none

**The owner's words:** "it's to become a factory for building agentic loops. All the loops it has currently have been used by many others, so they are example loops that the factory can reference when building future loops."

**For:** a factory that builds new agentic loops. [owner]
**For whom:** the owner's projects that need a loop (inferred).
**Success looks like:** a new loop for a new purpose is built by the factory, drawing on the example loops, rather than written from scratch (inferred: to be checked in the first strategy brief).
**Not:** the example loops are references, not the product; they aren't edited to become the factory (inferred from "example loops the factory can reference").

**State of knowledge**
- Known: the eight loop families here have been used by many projects [owner]; harnessv8 is one (initial_build.md); the other copies were lost in a reinstall [owner]; the owner's design notes (insights_for_loops.md) are in git.
- Probable: the design notes are input to how the factory builds loops (inferred).
- Unknown but relevant: what the factory is concretely (a loop of agents that builds loops? a method plus templates?), what it takes in and what it gives back; whether `data_to_improve_loops/` matters (the owner doesn't recall its origin).

### Stages toward the aim (the staircase)
main_effort: ST-2

#### ST-1 — settle the direction
order: 1
contributes: everything depends on it
state: grasped
alternatives: none
evidence: owner, 2026-10-18 (AIM-2)

#### ST-2 — define the factory: what it takes in, what it produces, how it uses the example loops
order: 2
contributes: the factory can't be built before it's defined
state: open
alternatives: to be drafted by the project agent in BR-3
evidence: none yet

(Further stages: drafted by the project agent in BR-3, from ST-2's outcome.)
