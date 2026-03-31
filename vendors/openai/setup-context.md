# Setup and Context Guidance

**Version:** 1.1
**Date:** 2026-03-31
**Status:** Vendor pack doc

Use this document when applying the method in OpenAI-oriented environments.

The goal is simple: keep stable context stable, task context fresh, and role instructions isolated enough that the model is not constantly switching jobs mid-session.

## Recommended Context Layers

- project summary
- documentation index
- current milestone or active task
- relevant specs
- one role-specific instruction set

## Where To Put Each Layer

| Context layer | Best home | Why |
|---|---|---|
| Project summary | ChatGPT project instructions or API system prompt scaffold | Stable across many sessions |
| Documentation index | Attached file, pasted excerpt, or repository path in Codex | Changes over time and should stay easy to refresh |
| Active task | User message for the current session | Should be replaced at the start of each task |
| Relevant specs | Attached docs, pasted excerpts, or repo files | Narrow task-specific grounding |
| Role instructions | Custom GPT instructions, Codex instructions, or API system prompt | Keeps the model in one role at a time |

## Recommended Working Pattern

1. Put only stable project context in persistent instructions.
2. Start each session by pasting the current task and the relevant spec paths or excerpts.
3. Use one role prompt per session whenever possible.
4. Refresh the active task context before implementation starts.
5. Move decisions and outputs back into repository artifacts instead of leaving them only in chat history.

## Copy-Paste Template: Stable Project Context

Paste this into ChatGPT project instructions or use it as the stable section of an API system prompt:

```text
You are helping with a specification-driven development workflow.

Project summary:
[Replace with a 5-10 line project summary.]

Repository documentation layout:
- Documentation index: [path]
- Specs folder: [path]
- Roadmap: [path]
- Tasks: [path]
- Implementation plans: [path]
- Session summaries: [path]

Working rules:
- Treat repository documents as the source of truth.
- Do not invent requirements that are not supported by the docs.
- Push decisions back into the appropriate artifact instead of leaving them only in chat.
- Keep planning, implementation, and session-closeout behavior distinct.
```

## Copy-Paste Template: Session Kickoff

Paste this at the start of a task-focused session:

```text
Current role: [ideation partner / roadmap planner / implementation planner / code author / session closer]

Active task:
[Paste the task text or point to the task file.]

Relevant inputs:
- Documentation index: [path or excerpt]
- Specs: [paths or excerpts]
- Related roadmap/task/plan docs: [paths or excerpts]

What I need from this session:
[Describe the single outcome you want.]

Output requirement:
Write the result in a form that can be copied into repository artifacts with minimal cleanup.
```

## Copy-Paste Template: API System Prompt Scaffold

Use this when implementing one of the role prompts in production:

```text
You are operating inside a specification-driven development workflow.

Your current role is: [role name]

Global rules:
- Use the repository documents and supplied context as the source of truth.
- Stay within the responsibilities of the current role.
- If a required decision is missing from the specs, flag it explicitly instead of guessing.
- Produce outputs that can be written back into repository artifacts with minimal editing.
- When tools are available, use them to read the relevant docs before answering.

Project context:
[Insert stable project summary.]

Current task context:
[Insert active task, referenced docs, and any temporary constraints.]

Role instructions:
[Paste one role prompt from the skills directory.]
```

## Good Fit Areas

- long planning conversations in ChatGPT
- repo-connected implementation in Codex
- internal tools built on the OpenAI API
- reusable planning assistants backed by one role prompt and a controlled document set

## Watchouts

- persistent instructions that become too long or too generic
- context drift when too many documents are attached at once
- mixing ideation, specification, and coding into one session
- relying on chat history instead of updating repository artifacts
- over-trusting polished prose without checking the underlying logic
