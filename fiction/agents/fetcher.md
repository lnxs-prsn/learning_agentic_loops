# AGENT 2 — FETCHER

**Role:** Reads the correct cards from /cards based on chapter type. Returns only the fields needed for this chapter. Never reads entire card files into context — queries specific fields only.

**Called by:** Orchestrator

---

## INPUT

- `chapter_type` — one of: new_focal_character / return_to_character:[char_id] / anchor_interlude / arc_transition
- `required_card_ids` — list of card IDs to fetch
- `required_fields` — list of fields per card

---

## FETCH LOGIC BY CHAPTER TYPE

### new_focal_character

```
Read from /state/master_state.json:
  - process_state_summary
  - macro_mystery_evidence
  - next_chapter_pointer

Read from /state/process_state.json:
  - For each operation: fields where current_touch = 0 or current_touch = 1 only
  - Do NOT read full operations list

Read from /core/concept_curriculum.md:
  - Current arc section only (arc matching master_state.arc_current)

Read from /cards/locations/[location_id].json (if location specified in pointer):
  - id, name, institutional_response, ordinary_life_texture, chapters_set_here

Read from /state/mystery_anchor.json:
  - observable_log last 3 entries ONLY
  - NEVER read hidden_coherence
```

### return_to_character:[char_id]

```
Read from /state/master_state.json:
  - process_state_summary
  - macro_mystery_evidence

Read from /cards/characters/[char_id].json:
  - Full card

Read from /cards/locations/[location_id].json (character's city):
  - Full card

Read from /state/process_state.json:
  - operation_due fields only

Read from /state/mystery_anchor.json:
  - observable_log last 3 entries ONLY
  - NEVER read hidden_coherence
```

### anchor_interlude

```
Read from /state/master_state.json:
  - Full document

Read from /state/mystery_anchor.json:
  - observable_log FULL
  - reader_can_suspect FULL
  - NEVER read hidden_coherence

Read from /state/process_state.json:
  - summary only (operation names and current_touch — no detail)

Read from /cards/locations/[relevant_ids].json:
  - All locations anchor has visited (derive from observable_log location fields)
  - Full cards for each
```

### arc_transition

```
Read from /arcs/arc_[N]_summary.md:
  - Previous arc summary (N = arc_current - 1, if arc_current > 1)

Read from /state/master_state.json:
  - Full document

Read from /state/process_state.json:
  - Full document

Read from /core/concept_curriculum.md:
  - Next arc section (arc_current + 1)
```

---

## OUTPUT FORMAT

Return a structured markdown block with each fetched field clearly labelled by source:

```markdown
## FETCHED FIELDS — Chapter [NNN] — [chapter_type]

### SOURCE: /state/master_state.json
process_state_summary: [value]
macro_mystery_evidence: [value]
next_chapter_pointer: [value]

### SOURCE: /state/process_state.json — operations_due
[operation_id]:
  name: [value]
  current_touch: [value]
  failure_modes_not_yet_shown: [value]
  contexts_not_yet_demonstrated: [value]

### SOURCE: /cards/characters/[char_id].json
[all fields]

### SOURCE: /state/mystery_anchor.json — observable_log (last 3)
[entries]

[etc.]
```

Pass this block to Assembler via Orchestrator.

---

## CRITICAL RULES

- Never return full card files. Return only the fields explicitly listed for each chapter type.
- NEVER read mystery_anchor.json hidden_coherence under any circumstances.
- If a card does not exist yet (new character), note it as MISSING — do not error.
- Never read /core/ documents except concept_curriculum.md, and only the current arc section.
- If a required field is absent from a card, return FIELD_MISSING:[field_name] — do not substitute.
