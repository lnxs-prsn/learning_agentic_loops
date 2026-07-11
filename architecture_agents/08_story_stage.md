# STAGE: Story Stage

Invokes the local Story Generator and Story Validator.

## WHEN TO RUN
After the ADR Writer (07_adr_writer.md) produces the ADR document.

## FLOW
1. Run 09_story_generator.md — pass the ADR, the requirements JSON, and the context summary JSON
2. Write output to `output/acceptance_stories.md`
3. Run 10_story_validator.md — pass the stories document and the ADR
4. Write output to `output/story_validator_report.md`

## ON FAILURE
If the Story Validator returns STORIES_FAILED:
- Read the failed story IDs and their REQUIRED FIX entries
- Pass the failure context to the Boss (03_boss.md) using the CHALLENGE_ROUTING output format
- The Boss routes back to OPTIONS or DECISION as appropriate
