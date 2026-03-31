# Production Implementation Guide

**Version:** 1.0
**Date:** 2026-03-31
**Status:** Vendor pack doc

Use this document when you want to turn the role prompts and workflow in this repository into a production OpenAI integration.

This guide assumes you are building an internal tool, developer workflow, or product feature that follows the same method phases as the rest of the repository.

## Implementation Goal

Build a system where:

- each method role is implemented as a distinct prompt or agent configuration
- repository documents are treated as the source of truth
- tools are used to fetch context instead of overloading prompts
- outputs are written back into repository artifacts or equivalent system records
- humans still review decisions, plans, and code changes

## Recommended Architecture

Use one role configuration per role instead of one giant assistant that does everything.

Recommended split:

- `ideation-partner`
- `roadmap-planner`
- `implementation-planner`
- `code-author`
- `session-closer`

For each role, define:

- a stable system prompt
- allowed tools
- expected inputs
- expected output shape
- rules for when to stop and ask for a human decision

## Tooling Strategy

There are two broad tool categories you should implement.

### 1. Your application tools

These are the tools that connect the model to your real system. Examples:

- `get_document(path)`
- `search_docs(query)`
- `list_tasks(milestone_id)`
- `write_artifact(path, content)`
- `get_repo_status()`
- `run_validation(command)`

Use these when you need controlled access to your own repository, docs, tickets, or internal systems.

### 2. OpenAI tool interfaces

Use the API's tool-calling support so the model can request those tools instead of hallucinating missing context.

Recommended production rules:

- Keep tool schemas narrow and explicit.
- Validate tool arguments server-side.
- Treat tool outputs as untrusted input and sanitize before reuse.
- Return structured tool results instead of prose when possible.
- Log tool calls so you can audit what context the model actually used.

## Hosted Tools Versus App Tools

Use OpenAI-hosted tools only where they directly help your workflow. Use your own application tools for source-of-truth project data.

A practical split:

- Use your own tools for repository docs, tasks, plans, and repo operations.
- Use hosted tools when you intentionally want capabilities such as web retrieval or other platform-provided actions.
- Do not let hosted tools replace your application's source-of-truth reads for project artifacts.

## Recommended Request Pattern

For each request:

1. Load the stable role prompt.
2. Pass only the active task context and the minimum supporting docs.
3. Provide the relevant tools for that role.
4. Require structured output for key artifacts when possible.
5. Persist the resulting artifact or summary outside the chat transcript.

## Example Role-to-Tool Mapping

| Role | Minimum useful tools | Why |
|---|---|---|
| Ideation partner | `get_document`, `write_artifact` | Reads notes and writes ideation artifacts |
| Roadmap planner | `get_document`, `search_docs`, `write_artifact` | Needs spec discovery plus roadmap output |
| Implementation planner | `get_document`, `search_docs`, `write_artifact` | Reads task/spec docs and writes a plan |
| Code author | `get_document`, `search_docs`, `get_repo_status`, `run_validation`, `write_artifact` | Needs repository-aware implementation support |
| Session closer | `get_repo_status`, `get_document`, `write_artifact` | Summarizes current work and updates records |

## Copy-Paste Example: Tool Definitions

Use small, explicit tool contracts. For example:

```json
{
  "type": "function",
  "name": "get_document",
  "description": "Read a repository document by path.",
  "parameters": {
    "type": "object",
    "properties": {
      "path": {
        "type": "string",
        "description": "Repository-relative path to the document."
      }
    },
    "required": ["path"],
    "additionalProperties": false
  }
}
```

```json
{
  "type": "function",
  "name": "write_artifact",
  "description": "Write approved markdown content to a repository artifact path.",
  "parameters": {
    "type": "object",
    "properties": {
      "path": {
        "type": "string"
      },
      "content": {
        "type": "string"
      }
    },
    "required": ["path", "content"],
    "additionalProperties": false
  }
}
```

## Structured Output Guidance

For production workflows, prefer structured outputs for artifacts that have predictable sections.

Good candidates:

- ideation notes
- roadmap summaries
- implementation plans
- session summaries

Use structured outputs to capture the shape, then render to markdown in your application layer if needed. This keeps downstream automation more reliable than parsing free-form prose.

## State Management Guidance

Do not rely on long chat transcripts as your primary memory.

Instead:

- store stable project context outside the conversation
- inject only the active task and relevant docs per request
- persist artifacts after each meaningful step
- pass back artifact paths or IDs in the next request

This keeps the workflow deterministic and easier to audit.

## Human Decision Gates

Make the model stop and escalate when:

- the spec is ambiguous in a way that changes scope
- a task is missing acceptance criteria
- implementation requires a risky production decision
- tool outputs conflict with the supplied specification
- code changes would exceed the approved plan

These should be explicit product rules, not just prompt suggestions.

## Suggested Production Rollout

1. Start with one non-coding role such as `implementation-planner`.
2. Implement only the minimum tools required to read docs and write one artifact type.
3. Add structured output validation.
4. Add repository-aware implementation only after the planning flow is stable.
5. Add session closeout last so task state stays synchronized.

## Operational Guardrails

- version your role prompts
- test prompts against real project artifacts, not toy examples
- keep tool permissions role-specific
- record which docs were read before each output
- require review before writing code or updating source-of-truth artifacts in production

## Related Docs

- [Setup and Context Guidance](setup-context.md)
- [Prompt Patterns](prompt-patterns.md)
- [Skills](skills/README.md)
