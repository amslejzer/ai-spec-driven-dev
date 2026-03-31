# Role Mapping

**Version:** 1.1
**Date:** 2026-03-31
**Status:** Vendor pack doc

This maps the core method roles to OpenAI-oriented usage patterns and calls out the best copy-paste target for each role prompt.

## Ideation Partner

- Best used in ChatGPT or a Custom GPT
- Best prompt target: project instructions plus a session kickoff message
- Focus on clarifying goals, constraints, risks, and early scope boundaries
- Best output target: `docs/ideation-notes.md` or equivalent repository notes

## Roadmap Planner

- Best used in ChatGPT, a Custom GPT, or an internal API-backed planning tool
- Best prompt target: one roadmap-specific role prompt plus attached spec docs
- Focus on milestones, phases, task breakdowns, and dependencies
- Best output target: `docs/roadmap.md` and task files in `docs/tasks/`

## Implementation Planner

- Best used in ChatGPT or an API-backed planning flow with access to task and spec documents
- Best prompt target: one implementation-planner prompt plus the active task and referenced specs
- Focus on acceptance criteria, test plan, affected files, and scope boundaries
- Best output target: `docs/plans/<task-id>-plan.md`

## Code Author

- Best used in Codex or another repository-connected coding agent
- Best prompt target: repository-connected coding instructions plus the implementation plan path
- Focus on implementing against the approved plan rather than re-deciding requirements
- Best output target: code changes, validation notes, and any required documentation updates

## Session Closer

- Best used in ChatGPT, Codex, or an API-backed internal closeout tool
- Best prompt target: one closeout prompt plus task path and current repo state
- Focus on summary, task updates, and commit-ready documentation changes
- Best output target: `docs/sessions/session-YYYY-MM-DD.md` and updated task files

## Recommended Surface By Phase

| Method phase | Best OpenAI surface | Why |
|---|---|---|
| Ideation | ChatGPT or Custom GPT | Interactive questioning and iterative refinement |
| Specification drafting | ChatGPT or API-backed doc assistant | Strong long-form drafting and revision |
| Roadmapping | ChatGPT or API-backed doc assistant | Good at structure, decomposition, and explicit assumptions |
| Implementation planning | ChatGPT or API-backed planning tool | Works well with narrow task context |
| Code implementation | Codex or repo-connected coding agent | Needs repository inspection, edits, and validation |
| Session closeout | ChatGPT, Codex, or API-backed closeout tool | Mostly summarization plus lightweight repo state handling |

## Practical Rule

If the role needs direct repository reads, code edits, or test execution, prefer Codex or another repository-connected agent. If the role mainly needs structured reasoning over documentation, ChatGPT or an API-backed tool is usually enough.
