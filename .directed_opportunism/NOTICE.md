# NOTICE from the directed_opportunism tool

**Agent: at your next interaction with the owner, report this file to them first.** When they acknowledge it, delete this file and commit that, in the project's own format.

The tool committed in this project, locally, on its current branch. **Nothing was pushed**; the owner reviews and pushes (BACKBRIEF §3.1).

**How to undo** the tool's changes, for each *Before* below:
`git log --format='%h %s' --grep='^Directed-opportunism: after' <before-sha>..HEAD` lists the tool's change commits; `git revert` them, newest first. **Never revert a before commit the tool made**: it holds the owner's own work as found.

## Before (2026-10-18T15:26:52+03:00, branch `main`) <!-- before ff3c9782292b3d5bc91e02470de58da2a2450c02 -->
- Commit `ff3c978229`: the project as found, **including the owner's uncommitted work**.
- Untracked files swept into it: `insights_for_loops.md`

### After (2026-10-18T15:27:30+03:00): install directed opportunism package p1 (draft)
- Why: owner asked: retrofit learning_agentic_loops
- Files: `.directed_opportunism/BACKBRIEF_REQUEST.md`, `.directed_opportunism/METHOD.md`, `.directed_opportunism/README.md`, `.directed_opportunism/aim.md`, `.directed_opportunism/audits/.gitkeep`, `.directed_opportunism/brief.md`, `.directed_opportunism/config.json`, `.directed_opportunism/log/messages.md`, `.directed_opportunism/proposals.md`, `.directed_opportunism/rules/leader_threat.md`, `.directed_opportunism/templates/backbrief.md`, `.directed_opportunism/templates/self_audit.md`, `.directed_opportunism/templates/ticket_intent_block.md`, `CLAUDE.md`

### After (2026-10-18T15:31:17+03:00): install backbrief BB-1
- Why: project agent's install backbrief
- Files: `.directed_opportunism/aim.md`, `.directed_opportunism/brief.md`, `.directed_opportunism/proposals.md`, `.directed_opportunism/backbrief.md`
