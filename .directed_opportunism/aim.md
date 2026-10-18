# Aim — learning_agentic_loops

What the project is for. METHOD §4. Field names compatible with the intent-anchoring kit (adapted from HC-4/HC-9).
**Status rule:** an agent drafts from evidence (`status: derived`); only the owner confirms (`status: confirmed`, with date). Never present a derived aim as confirmed. Append new versions; never rewrite a confirmed one; mark the old one `superseded_by`.

---

## AIM-1 — (open) what learning_agentic_loops is for
status: derived
confirmed: none
describes: 2026-10-18
evidence: folder tree (planning/delivery/debug/architecture/greenfield/migration agents, fiction/); delivery_agents/runner.md; initial_build.md; fiction_build_spec.md; insights_for_loops.md (owner's notes, untracked until the install's before commit ff3c978); data_to_improve_loops/planning_agents (differs from planning_agents/); one commit (71c9b34, 2026-07-11); owner, 2026-10-18: "not fully planned", "in hiatus", "its loops have been used by other projects (copied)", "no clear direction"
supersedes: none
superseded_by: none

**The owner has no settled direction for this project (owner, 2026-10-18), so this aim is not derived as one answer: below are candidate aims for the owner to pick or correct. Nothing is built toward any of them until one is confirmed.**

### Candidate aims (the owner picks one, or corrects)
- **C1 — A library of agentic loops that other projects copy.** For: well-defined multi-agent loops (planning, delivery, debug, architecture, greenfield, migration, fiction), each with its roles and state files, ready to copy into a project. For whom: the owner's other projects. Success: a project can pick a loop, copy it, and run it without redesigning it. Not: a framework or package that projects import; not tied to one project. Evidence: the `*_agents/` folders; runner.md ("thin router"); "used by other projects (copied)" (owner).
- **C2 — A lab for improving loop design from evidence.** For: test ideas about loop design (ecosystem over opponent, plan as continuous process, irrelevance management, the organism framework) against data from real runs, and feed what works back into the loops. For whom: the owner, and through them the projects that copy the loops. Success: a design idea is accepted or dropped on evidence from a real run. Not: writing more loops for their own sake. Evidence: insights_for_loops.md (sections "How to test it", "Open decisions", "Verdict"); data_to_improve_loops/ (a changed copy of planning_agents).
- **C3 — C1 now, C2 as the next stage** (inferred): keep the library usable as the main effort, and run design ideas as experiments against it. Evidence: both of the above exist side by side.
- (Not proposed, but possible: archive the project and leave the copies where they live. Evidence: hiatus. Listed so the choice is explicit.)

**State of knowledge**
- Known: seven loop families as role prompt files; a runner/boss/worker/reviewer/story-stage pattern repeats across them; example specs (initial_build.md: EPUB support for a podcast pipeline; fiction_build_spec.md); the owner's design notes; no README, no tests, no handoff; one commit.
- Probable: initial_build.md is a sample spec fed to the delivery loop (inferred: it's a phase/pass plan for another codebase); data_to_improve_loops/ holds a revised planning loop from real use (inferred: the files differ).
- Unknown but relevant: which projects copied which loops, and how they fared; whether the copies have since diverged (improvements made there and not brought back); which of C1–C3 the owner wants.

### Stages toward the aim (the staircase)
main_effort: ST-1

#### ST-1 — settle the direction
order: 1
contributes: everything else depends on which aim this is
state: open
alternatives: C1, C2, C3, archive
evidence: owner, 2026-10-18 ("no clear direction")

(Further stages are drafted once an aim is confirmed: the stages differ per candidate.)
