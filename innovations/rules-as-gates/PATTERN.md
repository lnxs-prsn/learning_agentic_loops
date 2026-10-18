# Rules-as-gates — a caution written as a test starts operating as a gate

## What it is
A discipline for projects that accumulate their own process rules. Every
safeguard is checked against one question — **can this be applied AFTER
generation, or does it decide whether generation happens at all?** — plus a
standing requirement that any bar **name what it concretely excludes**, and an
audit that keeps filters and producers from growing at the same rate.

The defect it names: a rule written in good faith as a *test* ("check that X
survives Y") is read by later sessions as a *gate* ("do not produce X until Y"),
and it then suppresses work invisibly. Nothing errors. Nothing is logged. The
work simply never gets written, and no one can see the absence.

## Problem it solves
Silent suppression by your own safeguards — the most expensive failure in a
rule-accumulating project, because it produces **no artifact to inspect**. A bad
rule that blocks output leaves the same trace as having had no ideas: an empty
folder. Teams therefore diagnose it as "we're not generating enough" and add
*more* process, which is the accelerant.

Three specific shapes it kills:
- **A caution executed as a prohibition** — "don't assume the reference
  implementation fits our case" gets implemented as *never read it*.
- **A provisionality marker executed as a brake** — "nothing here is decided
  yet" makes every artifact unbuildable-on, so nothing is ever founded.
- **A quality bar executed as an entry bar** — a standard meant to sort finished
  work gets applied before the work exists, so it is never produced.

## How to use it
1. **The after-generation test.** For every rule, ask: *can this be applied after
   the thing exists?* If yes, move it there explicitly — say so in the rule's own
   text, because the next reader will otherwise apply it earlier. **A rule that
   can only be applied before generation is the dangerous kind** and needs the
   scrutiny below.
2. **The exclusion requirement.** A bar must be able to say **what it concretely
   excludes**. *A bar that cannot name what it rules out is not ruling anything
   out* — it only radiates caution, which is what turns it into a gate. Keep a
   failing bar visible and **marked as failing** rather than deleting it; the
   marked entry is what stops it being re-added.
3. **Permission is the default.** State the admissible purpose positively and
   make exclusion require a *named* constraint. This inverts the burden: before,
   an agent meets a caution and wonders whether it is allowed (answer: no). After,
   it proceeds unless something names the exclusion.
4. **The apparatus audit.** Periodically count **filters vs producers** —
   rules, tests, bars, and checklists on one side; generators, prompts, and
   mining procedures on the other. They must not grow at the same rate. Watch for
   several filters added in a single sitting; that is the signature.
5. **The admission bar for new rules:** *adding a test requires naming the
   specific past mistake it would have caught.* If you cannot point at one, it is
   a preference, not a test. **Generators are free** — add as many as you like.
6. **Retire by salvage, never by deletion.** A rejected proposal usually contains
   a live part that is doing work elsewhere. Retire nothing without writing *the
   part of this that worked was ___*; if nothing did, write that too — knowing
   which are which is the point of the pass.

## Fits projects like
Any long-running project that writes its own operating rules: research and design
workspaces, agent-run repos with accumulating protocol, methodology-heavy teams,
anything with a `CONTRIBUTING`/`CONVENTIONS` surface that grows. Highest value
where **the product is generated rather than assembled** (ideas, designs,
content, specs), because there the suppressed output is invisible by construction.
Pairs with root-cause-laddering (that finds which *layer* a defect lives in; this
finds when the defect **is the safeguard**) and with decision-ledger (a rule that
survives this check is worth recording as a decision).

## Proven in
**Second origin project, 2026-07** — a conceptual-design workspace: one human
owner directing several AI agents (each with its own area in the repo, working
in sequence rather than concurrently), no code, product entirely generated prose.
Dated evidence:

- **2026-07-27, the audit that named the class.** After three blockers had been
  found and fixed, the owner asked what *else* might be blocking without anyone
  knowing. The audit found six, and four shared one shape — *a rule intended as a
  test operating as a gate*: (a) "don't assume the prior architecture fits" →
  **2,763 lines of directly relevant prior work went unread for the project's
  entire history**, its conclusions reconstructed from a verbal summary instead;
  reading it overturned four ideas in minutes. (b) "an analogy must survive hard
  material" → **no analogy was ever generated**, so the test never ran. (c) "this
  is not a decision" → nothing could be built on, and a competing project with
  *one* operational definition had built an architecture while this one held six
  provisional definitions and had built nothing. (d) "don't open the next phase
  prematurely" → that phase's work was being produced while the phase was
  formally refused.
- **2026-07-27/28, an entry bar corrected in place.** A promotion bar reading
  "be cheap to test" was, read literally, blocking every promotion. Corrected to
  *describe the refuting observation; you are not required to have made it* —
  the same rule moved from before generation to after.
- **2026-07-28, the apparatus audit, run once and immediately load-bearing.**
  Counted **31 method rules, 7 standing tests, 6 bar items, 8 commitments — and
  6 generators**, with five of the filters added in a single day. That count
  produced the "name what it would have caught" admission bar now in step 5.
- **2026-07-28, a housekeeping rule found to be destroying its own input.** *"Do
  not let ideas sit; promote, merge, or delete each one"* was deleting the raw
  material that generation ran on. Replaced by the salvage-line rule in step 6,
  after the owner's correction that a proposal which fails as a whole often has a
  part that works. Two of four already-closed ideas turned out to have live parts
  doing work elsewhere while the files sat marked closed.
- **2026-07-31, the owner supplied the structural antidote** — permission as the
  default plus *"a bar that cannot say what it excludes is not excluding
  anything."* Applied immediately to the project's own constraint list, where one
  long-standing entry is **kept in the file explicitly marked as failing the
  guard**, on the grounds that it had never excluded anything and would otherwise
  have become the seventh blocker. The pattern is applied to itself.
- **2026-07-31, two proposed standards killed within an hour of each other**, both
  for this defect: a fixed-question report template (its questions came from one
  day's reading, so later reports could only record movement along axes chosen
  while findings were preliminary) and an answer-the-previous-report rule (it made
  the previous reading the reference frame, so a wrong reading would propagate by
  being the thing everything was written against). The reasoning was kept in place
  rather than discarded, which is what stops them being re-proposed.

**Known limit, stated in the origin workspace:** the permission-default rule
protects against gates built out of *cautions*. It does **not** protect against a
gate built out of a genuine constraint applied too early — so step 1 stays a
habit and is not retired by step 3.

## Kit (deployable files in `kit/`)
`kit/GATE-CHECK.md` — the one-page check: the four questions to run on any rule,
the filters-vs-producers audit, and the retire-by-salvage line. Run it when
adding a rule, and as a sweep when output has gone quiet.
