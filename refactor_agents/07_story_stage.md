# STAGE: Story Stage

Invokes the local Story Generator and Story Validator.

## WHEN TO RUN
After the Equivalence Checker (06_equivalence_checker.md) returns EQUIVALENT — but only if the task queue JSON contains a `story_routing` section with one or more entries. If `story_routing` is absent or empty, skip this stage entirely.

## FLOW
1. Run 08_story_generator.md — pass task queue JSON, spec, entry point files from `story_routing`
2. Write output to `output/acceptance_stories.md`
3. Run 09_story_validator.md — pass the stories document and the same source files
4. Write output to `output/story_validator_report.md`

## ON FAILURE
If the Story Validator returns STORIES_FAILED:
- Read `Responsible spec passes` from the verdict
- Pass the failure context to the Boss (03_boss.md) using the EQUIVALENCE_FAILURE_ANALYSIS output format
- The Boss determines which refactor to revise or revert
