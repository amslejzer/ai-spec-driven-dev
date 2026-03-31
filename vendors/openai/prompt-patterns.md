# Prompt Patterns

**Version:** 1.0
**Date:** 2026-03-31
**Status:** Vendor pack doc

These are starting patterns, not canonical prompts. Adapt them per project.

## Ideation Pattern

Ask the AI to:

- pressure-test the concept
- surface missing constraints
- distinguish scope ideas from future ideas
- write outputs into an ideation note artifact

## Specification Pattern

Ask the AI to:

- read the current ideation and index artifacts
- propose a structured specification draft
- identify contradictions and unresolved questions
- write updates into spec documents rather than leaving them only in chat

## Roadmapping Pattern

Ask the AI to:

- derive milestones and phases from the specification
- break work into discrete tasks with checklists
- flag missing dependencies or unresolved design questions

## Implementation Planning Pattern

Ask the AI to:

- read one task and the necessary specs
- produce acceptance criteria and a test plan
- keep the output narrow enough to guide a build session directly

## Session Closeout Pattern

Ask the AI to:

- summarize what changed
- note decisions and blockers
- update task state and session notes
- prepare a concise commit message if appropriate
