# AGENT 3 — ASSEMBLER

**Role:** Takes fetched fields and arranges them into a clean prose generation prompt. Writes /prompts/assembled_prompt.md. The Writer subagent receives only this file.

**Called by:** Orchestrator, after Fetcher and Consistency Checker have run.

---

## INPUT

- Fetched fields block (from Fetcher)
- `chapter_type`
- Consistency Checker report (flags only — do not include in assembled prompt)

---

## ASSEMBLY PROCEDURE

```
1. Read /core/style_contract.md
   Extract: Rule 1, Rule 2, Rule 3 verbatim
   Extract: never list verbatim

2. Read /core/world_rules.md
   Extract: the 6 world rules verbatim

3. Determine chapter number from fetched master_state.json chapter_count + 1

4. Build assembled_prompt.md using the structure below

5. Apply any FLAG corrections from consistency report:
   - If a failure_mode was already shown: pick the next one from process_state failure_modes_not_yet_shown
   - If operation re-explanation flagged: remove explanatory framing, keep physical anchor only
   - If anchor appearance too frequent: set anchor appearance to No

6. Write the complete file to /prompts/assembled_prompt.md

7. Report to Orchestrator: assembled_prompt.md written, chapter number confirmed
```

---

## assembled_prompt.md STRUCTURE

```markdown
# CHAPTER [NNN] — GENERATION PROMPT

## VOICE RULES
[Rule 1 verbatim from style_contract.md]
[Rule 2 verbatim from style_contract.md]
[Rule 3 verbatim from style_contract.md]

### Never:
[Never list verbatim from style_contract.md]

## WORLD RULES
[Rule 1 verbatim from world_rules.md]
[Rule 2 verbatim from world_rules.md]
[Rule 3 verbatim from world_rules.md]
[Rule 4 verbatim from world_rules.md]
[Rule 5 verbatim from world_rules.md]
[Rule 6 verbatim from world_rules.md]

## THIS CHAPTER

**Chapter type:** [new_focal_character / return_to_character / anchor_interlude / arc_transition]
**Chapter number:** [NNN]

**Focal character:**
[If new: name, occupation, city, situation — generated fresh by Assembler, consistent with world rules]
[If returning: paste name, occupation, city, ordinary_life_state, gate_history summary, still_gets_wrong from character card]

**Gate this chapter:**
[Grade from process_state difficulty_rating]
[Problem structure: unknown / data / condition — derive from operation being taught]
[Wrong approach to show first — pull from failure_modes_not_yet_shown]
[Correct approach that closes gate — derive from operation]

**Operation being taught:**
[Operation name]
[Touch number: current_touch + 1]
[Delivery channel: narrator label / character action / observer note — vary by touch number]
[Physical anchor: pull from /cards/concept/[operation_id].json physical_anchor]

**Operations to use naturally (no re-explanation):**
[List all operations where character's comprehension_state shows owned = true]
[For each: operation name + physical anchor only]

**Ordinary life echo:**
[Real-world problem that mirrors the gate structure — derive from correspondence_map.md]
[Must appear in same chapter as gate closes]

**Anchor character appearance:**
[Yes / No — from next_chapter_pointer anchor_appears]
[If Yes: what they observe described observationally only, no interiority]
[Pull from observable_log to establish continuity — never reference hidden_coherence]

**Failure mode to demonstrate:**
[Specific failure mode from failure_modes_not_yet_shown for this operation]
[Must appear before correct approach]

**Macro mystery:**
[Evidence to plant: pull from master_state.json macro_mystery_evidence if applicable]
[How it appears: present without explanation]

**Emotional beat:**
[Character's internal arc this chapter — derive from ordinary_life_state and gate_history]

**Foreshadowing:**
[Optional: seed for next chapter pointer if applicable]

## CONSTRAINTS
- Do not name the operation before the character has suffered its absence
- Do not close the gap between observation and meaning
- The anchor character's hidden coherence is never surfaced
- Failure before success always
- Ordinary life echo must feel inevitable not surprising
- Chapter ends when the gate closes and the ordinary life echo lands
- Length: 2000-3000 words
```

---

## CRITICAL RULES

- Never include hidden_coherence content in the assembled prompt under any circumstances.
- Never include the Consistency Checker report in the assembled prompt.
- Never include raw card file contents — extract and reframe fields only.
- The assembled prompt must be self-contained. The Writer subagent receives nothing else.
- If a required field is MISSING from fetched data, fill with [MISSING — generate consistent with world] rather than leaving blank.
- Do not modify /core/ documents.
