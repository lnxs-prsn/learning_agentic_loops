# NOTICE from the directed_opportunism tool

**Agent: at your next interaction with the owner, report this file to them first.** When they acknowledge it, delete this file and commit that, in the project's own format.

The tool committed in this project, locally, on its current branch. **Nothing was pushed**; the owner reviews and pushes (BACKBRIEF §3.1).

**How to undo** the tool's changes, for each *Before* below:
`git log --format='%h %s' --grep='^Directed-opportunism: after' <before-sha>..HEAD` lists the tool's change commits; `git revert` them, newest first. **Never revert a before commit the tool made**: it holds the owner's own work as found.

## Before (2026-10-18T16:05:00+03:00, branch `main`) <!-- before 2edfb6b127d959b28ca2a87d2277221dcb418d94 -->
- Commit `2edfb6b127`: no before commit was needed (nothing uncommitted); this is just the starting point, not a tool commit.
- Untracked files swept into it: none

### After (2026-10-18T16:05:20+03:00): record owner's sitting answers: aim confirmed (factory)
- Why: install sitting: owner confirmed the aim and acknowledged the notice
- Files: `.directed_opportunism/aim.md`, `.directed_opportunism/log/messages.md`

### After (2026-10-18T16:05:38+03:00): fix dropped text in owner-answer log entry
- Why: a quoting slip dropped the folder name from MSG-1 item 5
- Files: `.directed_opportunism/log/messages.md`

### After (2026-10-18T16:06:59+03:00): integrate directed opportunism (p1): README, copies list
- Why: accepted install backbrief BB-1 (MSG-2), plan items 4-6
- Files: `.directed_opportunism/config.json`, `.directed_opportunism/log/messages.md`, `.directed_opportunism/copies.md`, `README.md`
