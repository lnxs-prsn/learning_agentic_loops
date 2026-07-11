# STAGE: Story Stage

Invokes the local Story Generator and Story Validator.

## WHEN TO RUN
After the Integrator (07_integrator.md) returns ALL_PASS.

## FLOW
1. Run 09_story_generator.md — pass task queue JSON, spec, entry point files from `story_routing`
2. Write output to `output/acceptance_stories.md`
3. Run 10_story_validator.md — pass the stories document and the same source files
4. Write output to `output/story_validator_report.md`

## ON FAILURE
If the Story Validator returns STORIES_FAILED:
- Read `Responsible spec passes` from the verdict
- Look up those passes in `story_routing` to find the task responsible
- Pass the failure context to the Boss (03_boss.md) using the FAILURE_ROUTING output format
- The Boss identifies which task to re-open and what the Builder needs to fix
