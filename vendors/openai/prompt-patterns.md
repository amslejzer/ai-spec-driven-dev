# Prompt Patterns

**Version:** 1.1
**Date:** 2026-03-31
**Status:** Vendor pack doc

These are copy-paste starter prompts. They are intentionally concrete so teams can use them immediately, then refine them through real project use.

Replace bracketed placeholders before use.

## Ideation Pattern

Best pasted into a ChatGPT session or the user message of an API call.

```text
Act as an ideation partner for a specification-driven development workflow.

I want to explore this project idea:
[paste idea]

Context:
- Audience: [audience or "unknown"]
- Constraints: [constraints]
- Existing notes: [notes or paths]

Your job:
- Ask the smallest useful set of clarifying questions first.
- Pressure-test assumptions and surface hidden risks.
- Separate first-version scope from future ideas.
- Convert the useful conclusions into structured ideation notes I can copy into the repository.

Output format:
- Clarifying questions
- Risks and unknowns
- Proposed first-version scope
- Out-of-scope ideas
- Draft ideation note
```

## Specification Pattern

Best pasted into ChatGPT or an API-backed documentation assistant with the relevant docs attached.

```text
Act as a specification drafter for a specification-driven development workflow.

Read these inputs:
- Documentation index: [path or excerpt]
- Ideation notes: [path or excerpt]
- Related notes: [paths or excerpts]

Your job:
- Draft or refine the specification using the supplied artifacts as the source of truth.
- Identify contradictions, unanswered questions, and places where requirements are too vague.
- Keep the spec concrete enough to support roadmap and implementation planning later.
- Write in repository-friendly markdown instead of conversational prose.

Output format:
- Spec gaps or contradictions
- Proposed specification draft
- Open questions requiring human decision
```

## Roadmapping Pattern

Best pasted into ChatGPT, a Custom GPT, or an API-backed planning tool.

```text
Act as a roadmap planner for a specification-driven development workflow.

Read these inputs:
- Documentation index: [path or excerpt]
- Specification documents: [paths or excerpts]
- Current project state: [summary]

Your job:
- Derive milestones from the specification.
- Break milestones into phases and discrete tasks.
- Include dependencies, sequencing assumptions, and blocking spec gaps.
- Keep tasks small enough to support focused implementation sessions.

Output format:
- Roadmap summary
- Milestones with completion signals
- Phases and tasks
- Risks and blockers
```

## Implementation Planning Pattern

Best pasted into ChatGPT or an API-backed planner with the task doc attached.

```text
Act as an implementation planner for a specification-driven development workflow.

Read these inputs:
- Task document: [path or excerpt]
- Relevant specs: [paths or excerpts]
- Documentation index: [path or excerpt]

Your job:
- Define what done means in testable terms.
- Produce acceptance criteria scoped only to this task.
- Produce a focused test plan covering happy path, edge cases, and failure cases.
- Identify likely files or systems affected.
- List unresolved issues instead of guessing.

Output format:
- Summary
- Approach
- Acceptance criteria
- Test plan
- Open issues
```

## Code Author Pattern

Best pasted into Codex or another repository-connected coding agent.

```text
Act as a code author for a specification-driven development workflow.

Read these inputs before editing:
- Implementation plan: [path]
- Task document: [path]
- Relevant specs: [paths]

Your job:
- Inspect the repository before editing.
- Implement the smallest complete change that satisfies the implementation plan.
- Stay within scope.
- Reuse existing patterns instead of creating speculative abstractions.
- Run or clearly describe validation against the plan's acceptance criteria.

Output format:
- Files changed
- Validation performed
- Acceptance criteria status
- Follow-up notes
- Suggested commit message
```

## Session Closeout Pattern

Best pasted into ChatGPT, Codex, or an API-backed closeout tool.

```text
Act as a session closer for a specification-driven development workflow.

Session inputs:
- Active task: [path or summary]
- Work completed: [summary]
- Files changed: [list]
- Decisions made: [list]
- Open blockers: [list]

Your job:
- Summarize what changed.
- Record decisions and blockers.
- Update task state if enough information is available.
- Prepare closeout text that can be copied into a session summary document.
- Suggest a concise commit message if appropriate.

Output format:
- Work completed
- Decisions made
- Issues or blockers
- Repo updates
- Recommended next step
- Suggested commit message
```
