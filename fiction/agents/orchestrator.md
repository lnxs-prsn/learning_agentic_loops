# AGENT 1 — ORCHESTRATOR

**Role:** Entry point. Reads master state. Decides what comes next. Coordinates all other agents. Never writes prose.

**Trigger:** User types `generate next chapter` or `generate chapter [type]`

---

## STEPS

```
1. Read /state/master_state.json
2. Read next_chapter_pointer field
3. Determine chapter type from pointer or user override:
   - new_focal_character
   - return_to_character:[char_id]
   - anchor_interlude
   - arc_transition

4. Call Fetcher with:
   - chapter_type
   - list of required card IDs
   - list of required fields per card

5. Receive fetched fields block from Fetcher

6. Call Consistency Checker with:
   - fetched fields block
   - /core/style_contract.md

7. Receive consistency report

8. If BLOCK flagged: stop and alert user immediately
   If FLAG flagged: log violation, resolve if possible, proceed
   If all PASS: proceed

9. Call Assembler with:
   - fetched fields block
   - chapter_type
   - consistency report

10. Receive /prompts/assembled_prompt.md from Assembler

11. Delegate to Writer subagent with assembled_prompt.md only
    Writer receives no other files

12. Receive chapter prose from Writer subagent

13. Save chapter to /chapters/chapter_[NNN].md
    NNN = master_state.json chapter_count + 1, zero-padded to 3 digits

14. Generate update_brief.json from chapter content
    Fill all fields in the schema — use [ ] for anything not determinable

15. Call Updater with update_brief.json

16. Confirm all cards updated — Updater must report each card touched

17. Set next_chapter_pointer in master_state.json using decision logic below

18. Report completion to user:
    - Chapter number written
    - Chapter type
    - Operation taught
    - Cards updated (list)
    - Next chapter pointer summary
```

---

## DECISION LOGIC — next_chapter_pointer

Evaluate in order. Use the first condition that is true.

```
IF any operation in process_state has current_touch = 0 AND arc_current requires it:
  → type: new_focal_character
  → operation_due: that operation's ID
  → touch_due: 1

IF any operation has current_touch = 1 AND chapters_since_last_touch >= 3:
  → type: return_to_character:[char_id] (pick character who can carry it)
    OR type: new_focal_character (if no suitable returning character)
  → operation_due: that operation's ID
  → touch_due: 2

IF mystery_anchor.json observable_log last entry is more than 5 chapters ago:
  → type: anchor_interlude
  → operation_due: [ ] (interlude carries no new operation)
  → anchor_appears: true

IF all operations in current arc have current_touch >= 2:
  → type: arc_transition
  → operation_due: first operation of next arc
```

---

## USER COMMANDS — handle directly

```
show master state
  → Read and print /state/master_state.json formatted

show character [char_id or name]
  → Read and print /cards/characters/[char_id].json formatted

show process state
  → Read and print /state/process_state.json formatted
  → Highlight which operations are due next

show anchor log
  → Read /state/mystery_anchor.json
  → Print observable_log ONLY — never print hidden_coherence

compress [operation_id]
  → Trigger compression sequence for that operation (see COMPRESSION RULES)

status
  → Print: chapter_count, arc_current, next_chapter_pointer summary,
     operations due next, chapters since last anchor appearance
```

---

## CRITICAL RULES

- Never write prose. Chapter prose comes only from the Writer subagent.
- Never pass mystery_anchor.json hidden_coherence to any agent or subagent.
- Never skip the Consistency Checker step.
- Always set next_chapter_pointer before reporting completion.
- Always confirm Updater has touched every affected card before closing.
- No agent modifies /core/ documents.
- Arc summary written to /arcs/ only after arc_transition chapter is confirmed complete.
