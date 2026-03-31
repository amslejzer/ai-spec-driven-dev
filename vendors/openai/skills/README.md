# OpenAI Skills

**Version:** 1.1
**Date:** 2026-03-31
**Status:** Vendor pack doc

These files are copy-paste role prompts for OpenAI-oriented workflows.

They are not tied to a single OpenAI surface. You can paste them into:

- ChatGPT project instructions
- Custom GPT instructions
- Codex instructions for repository-connected work
- API system prompts for internal tools or products

## How To Use These Files

1. Choose one role for the current session or workflow step.
2. Copy the contents of that role file into your chosen prompt target.
3. Pass the active task and relevant document paths or excerpts as the current session input.
4. Write the output back into the repository artifact that belongs to that role.

## Recommended Pairings

| Skill | Best OpenAI surface | Typical input |
|---|---|---|
| [ideation-partner.md](ideation-partner.md) | ChatGPT or Custom GPT | Raw project idea, notes, constraints |
| [roadmap-planner.md](roadmap-planner.md) | ChatGPT, Custom GPT, or API | Spec docs and documentation index |
| [implementation-planner.md](implementation-planner.md) | ChatGPT or API | Task doc plus relevant specs |
| [code-author.md](code-author.md) | Codex or repo-connected coding agent | Implementation plan plus repository access |
| [session-closer.md](session-closer.md) | ChatGPT, Codex, or API | Task path, repo state, decisions, blockers |

## Important Usage Rule

Use one role prompt at a time. The method works best when the assistant is not trying to ideate, plan, code, and close the session all in one instruction set.

## Adaptation

These prompts are starting points, not frozen text. Adapt them as real usage reveals missing guidance, unnecessary detail, or role-specific needs in your environment.
