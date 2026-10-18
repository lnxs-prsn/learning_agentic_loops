# GATE CHECK — is this safeguard suppressing the work it was meant to improve?

Run it **when adding any rule**, and as a **sweep whenever output has gone
quiet** — because this defect produces no error, no log, and no artifact. An
empty folder looks identical whether the rule blocked the work or nobody had
ideas. That ambiguity is the whole problem.

## The four questions

**1. Can this be applied AFTER the thing exists?**
- Yes → **say so in the rule's own text.** The next reader will apply it earlier
  than you intended unless the rule states its own timing.
- No → this is the dangerous kind. It decides whether work happens at all.
  Justify it explicitly or drop it.

**2. What does this bar concretely exclude?**
Name a specific thing it rules out. If you cannot:
- it is not excluding anything — it is only radiating caution,
- and caution with no named exclusion is what turns a test into a gate.
- **Keep it, marked as failing this check.** A deleted bad bar comes back; a
  bar visibly marked as failing does not.

**3. Is permission the default here?**
State the admissible purpose **positively**, and make exclusion require a
**named** constraint.

```
before   a caution exists → the worker wonders whether it is allowed → it isn't
after    permitted by default → a constraint must be NAMED to remove it
```

**4. What specific past mistake would this have caught?**
Point at one. If you cannot, it is a preference, not a test — file it as such.
**Generators are free.** This bar applies only to things that filter.

## The apparatus audit

Count them. They must not grow at the same rate.

```
FILTERS     rules · tests · bars · checklists · conventions · gates
PRODUCERS   generators · mining procedures · prompts · elicitation methods
```

**Signature of trouble:** several filters added in one sitting; a ratio drifting
past a few filters per producer; or "we aren't generating enough" being answered
with more process. That answer is the accelerant, not the fix.

**Asymmetry to remember:** a wrong filter suppresses work *invisibly*. A wrong
generator produces something bad, which you can see and discard. They are not
symmetric risks and must not carry symmetric caution.

## Retire by salvage, never by deletion

Before retiring any rejected proposal, write:

> **The part of this that worked was ___.**

If nothing did, write *that*. A proposal that fails as a whole routinely contains
a live part already doing work somewhere else — and deleting the file deletes the
material the next round generates from.

## The three shapes to watch for

| The rule says | It gets executed as | Cost |
|---|---|---|
| "don't assume prior work fits" | **never read the prior work** | re-derive what was solved; the caution never even applied |
| "this isn't decided yet" | **nothing can be built on** | no foundations; competitors with one working definition ship |
| "must clear a quality bar" | **applied before the work exists** | the bar never runs, because nothing reaches it |

## The one that is not covered

Permission-by-default kills gates built out of **cautions**. It does not kill a
gate built out of a **genuine constraint applied too early**. Keep question 1 as
a habit; question 3 does not retire it.
