# OpenAI Skills

**Version:** 1.2
**Date:** 2026-04-24
**Status:** Vendor pack doc

These files are copy-paste role prompts for OpenAI-oriented workflows.

They are not tied to a single OpenAI surface. The same role prompt can be pasted into:

- ChatGPT project instructions
- Custom GPT instructions
- Codex CLI sessions and `AGENTS.md`
- Codex cloud (the ChatGPT-integrated coding agent) via committed `AGENTS.md`
- OpenAI API system prompts for internal tools or products

## Installation

See [install.md](install.md) for the full install guide, including the dependency problem (method vocabulary and template references that do not travel with the prompt) and per-surface install recipes for each of the targets above.

## Recommended Pairings

| Skill | Best OpenAI surface | Typical input |
|---|---|---|
| [ideation-partner.md](ideation-partner.md) | ChatGPT or Custom GPT | Raw project idea, notes, constraints |
| [roadmap-planner.md](roadmap-planner.md) | ChatGPT, Custom GPT, or API | Spec docs and documentation index |
| [implementation-planner.md](implementation-planner.md) | ChatGPT or API | Task doc plus relevant specs |
| [code-author.md](code-author.md) | Codex CLI or Codex cloud | Implementation plan plus repository access |
| [session-closer.md](session-closer.md) | ChatGPT, Codex, or API | Task path, repo state, decisions, blockers |

## Included Context

| File | Purpose |
|---|---|
| [install.md](install.md) | Installation guide and per-surface recipes |
| [method-primer.md](method-primer.md) | Condensed method context shipped alongside the role prompts |

## Important Usage Rule

Use one role prompt at a time. The method works best when the assistant is not trying to ideate, plan, code, and close the session all in one instruction set.

## Adaptation

These prompts are starting points, not frozen text. Adapt them as real usage reveals missing guidance, unnecessary detail, or role-specific needs in your environment.
