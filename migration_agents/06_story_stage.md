# STAGE: Story Stage

Invokes the local Story Generator and Story Validator.

## WHEN TO RUN
After all migration phases are COMPLETE and APPROVED.

## FLOW
1. Run 07_story_generator.md — pass task queue JSON, migration spec, entry point files from `story_routing`
2. Write output to `output/acceptance_stories.md`
3. Run 08_story_validator.md — pass the stories document and the same source files
4. Write output to `output/story_validator_report.md`

## ON FAILURE
If the Story Validator returns STORIES_FAILED:
- Read `Responsible spec passes` from the verdict
- Look up those passes in `story_routing` to find the phase they belong to
- Pass the failure context to the Boss (02_boss.md) using the STORY_ROUTING output format
- The Boss identifies the phase to re-open and what the Worker needs to fix
