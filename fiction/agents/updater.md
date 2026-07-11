# AGENT 5 — UPDATER

**Role:** Receives update_brief.json from Orchestrator after chapter is written. Updates all relevant cards and state files. Never reads the full chapter prose — works from update_brief.json only.

**Called by:** Orchestrator, after Writer subagent returns chapter.

---

## INPUT

- /prompts/update_brief.json
- List of affected card IDs (from Orchestrator)

---

## UPDATE SEQUENCE

Execute in this order. Report each step to Orchestrator as it completes.

```
STEP 1 — Character card
  IF update_brief.focal_character.is_new = true:
    Create /cards/characters/[char_id].json using character schema
    Populate from update_brief focal_character fields
    Set first_appeared to chapter number
    Set last_seen to chapter number
    Set gate_history to [gate_visited object]

  IF update_brief.focal_character.is_new = false:
    Read /cards/characters/[char_id].json
    Append gate_visited to gate_history array
    Apply comprehension_changes to comprehension_state
    Update ordinary_life_state if changed
    Update last_seen to chapter number
    Update still_gets_wrong if applicable
    Write updated card

STEP 2 — Concept/operation card
  Read /cards/concept/[operation_id].json
  Increment current_touch by 1
  Append to teaching_history:
    { chapter: NNN, char_id: [id], touch: N, context: [context] }
  Append failure_mode_shown to failure_modes_shown array
  Remove failure_mode_shown from failure_modes_not_yet_shown array
  Append context_demonstrated to contexts_demonstrated array
  Remove from contexts_not_yet_demonstrated array
  IF update_brief.process_updates.transferred = true:
    Set transferred_to_ordinary_life = true
  IF current_touch reaches compressible_at_touch (default 3):
    Flag for compression in master_state (see COMPRESSION)
  Write updated card

STEP 3 — Event card
  Create /cards/events/[gate_id].json using event schema
  Set chapter_opened to chapter number
  Set status to "open"
  Populate from gate_visited fields in update_brief
  IF gate is closed in this chapter:
    Set chapter_closed to chapter number
    Set status to "closed"
    Move file to /cards/events/archive/[gate_id].json
    Delete original from /cards/events/

STEP 4 — Location card
  Read /cards/locations/[location_id].json
  Append chapter number to chapters_set_here array
  IF update_brief.location_updates.new_texture is non-empty:
    Append each entry to ordinary_life_texture array
  Write updated card

STEP 5 — Mystery anchor
  IF update_brief.anchor_update.appeared = true:
    Read /state/mystery_anchor.json
    Append to observable_log:
      { chapter: NNN, observation: [text], location: [location_id] }
    Write updated file

STEP 6 — Macro mystery
  IF update_brief.macro_mystery_update.evidence_planted = true:
    Read /state/master_state.json
    Append to macro_mystery_evidence array:
      { chapter: NNN, evidence: [text] }
    [Write in STEP 7 with other master_state changes]

STEP 7 — master_state.json
  Read /state/master_state.json
  Increment chapter_count by 1
  Apply process_state_summary update:
    IF operation current_touch < 3:
      Update operation entry with new touch number and last chapter
    IF operation current_touch reaches 3 (COMPRESSION):
      Replace full operation object with single string:
        "[operation_id]": "touch_3_owned"
  Update population_index:
    IF new character: append { id: [char_id], name: [name], status: "active", last_seen: NNN }
    IF returning character: update last_seen
    IF character not seen in 20+ chapters: set status to "dormant"
  Append macro_mystery_update if applicable (from STEP 6)
  Write next_chapter_pointer from update_brief.next_chapter_pointer
  Write updated master_state.json

STEP 8 — process_state.json
  Read /state/process_state.json
  Apply same updates as concept card:
    Increment current_touch
    Update failure_modes_shown / failure_modes_not_yet_shown
    Update contexts_demonstrated / contexts_not_yet_demonstrated
    Update transferred_to_ordinary_life
  Write updated process_state.json

STEP 9 — Arc summary (arc_transition only)
  IF chapter_type = arc_transition:
    Write /arcs/arc_[N]_summary.md
    Include: arc number, operations taught, touch levels reached,
             characters introduced, macro_mystery_evidence planted,
             anchor appearances, total chapters
    Only write after Orchestrator confirms arc is complete

STEP 10 — Report
  Report to Orchestrator:
    - List every file touched
    - Confirm next_chapter_pointer is written
    - Flag any MISSING fields that could not be filled
    - Flag any COMPRESSION events triggered
```

---

## COMPRESSION RULES

When an operation reaches touch_3:
```
1. In master_state.json process_state_summary:
   Replace: "[operation_id]": { full object }
   With:    "[operation_id]": "touch_3_owned"

2. Full detail remains in /cards/concept/[operation_id].json — do NOT modify it

3. In population_index, character entries not seen in 20+ chapters:
   Replace: { id, name, status: "active", last_seen: NNN, ... }
   With:    { "id": "[char_id]", "name": "[name]", "status": "dormant", "last_seen": NNN }
   Full character card remains in /cards/characters/ — do NOT modify it
```

---

## update_brief.json SCHEMA

The Updater expects this exact structure from Orchestrator:

```json
{
  "chapter": "NNN",
  "chapter_type": "new_focal_character",
  "focal_character": {
    "id": "char_XXX",
    "is_new": true,
    "name": "[ ]",
    "occupation": "[ ]",
    "city": "[ ]",
    "gate_visited": {
      "gate_id": "G-XXX",
      "grade": 1,
      "operation_encountered": "[ ]",
      "approach_taken": "[ ]",
      "understood": false,
      "looked_back": false,
      "transferred_to_life": false
    },
    "comprehension_changes": {},
    "ordinary_life_state": "[ ]"
  },
  "process_updates": {
    "operation": "[ ]",
    "new_touch": 1,
    "failure_mode_shown": "[ ]",
    "context_demonstrated": "[ ]",
    "transferred": false
  },
  "location_updates": {
    "location_id": "[ ]",
    "new_chapter_added": "NNN",
    "new_texture": []
  },
  "anchor_update": {
    "appeared": false,
    "observation": "[ ]",
    "location": "[ ]"
  },
  "macro_mystery_update": {
    "evidence_planted": false,
    "evidence": "[ ]"
  },
  "next_chapter_pointer": {
    "chapter": "NNN+1",
    "type": "[ ]",
    "operation_due": "[ ]",
    "touch_due": 0,
    "failure_mode_to_show": "[ ]",
    "anchor_appears": false
  }
}
```

---

## CRITICAL RULES

- Never read the full chapter prose. Work from update_brief.json only.
- Never modify /core/ documents.
- Report every file touched — Orchestrator cannot confirm completion without this list.
- If update_brief has missing required fields: complete what is possible, flag the gap.
- Event cards that close in this chapter move to /cards/events/archive/ immediately.
- next_chapter_pointer must be written to master_state.json before reporting complete.
