# Anthropic Skills

**Version:** 1.2
**Date:** 2026-03-31
**Status:** Vendor pack doc

These are Claude Code skill files that can be copied into any project's `.claude/commands/` directory and used as slash commands.

## Usage

Copy any skill file into your project:

```
cp vendors/anthropic/skills/ideation-partner.md /path/to/your-project/.claude/commands/
```

Then invoke it in Claude Code:

```
/project-setup A reading tracker app for personal use
/ideation-partner A reading tracker app for personal use
/roadmap-planner docs/specification.md
/implementation-planner docs/tasks/M1-P1-T1.md
/code-author docs/plans/M1-P1-T1-plan.md
/session-closer docs/tasks/M1-P1-T1.md
```

## Included Skills

| Skill | Phase | Purpose |
|-------|-------|---------|
| [project-setup.md](project-setup.md) | Setup | Take an empty folder to a method-ready project |
| [ideation-partner.md](ideation-partner.md) | Ideation | Refine a concept before specification |
| [roadmap-planner.md](roadmap-planner.md) | Roadmapping | Turn specs into milestones and tasks |
| [implementation-planner.md](implementation-planner.md) | Planning | Turn a task into a build-ready plan |
| [code-author.md](code-author.md) | Implementation | Implement against an approved plan |
| [session-closer.md](session-closer.md) | Any | Capture session results for continuity |

## Adaptation

These skills are starting points. Adapt them as real usage reveals gaps or unnecessary detail. The behavioral instructions in each skill are drawn from the methodology's core principles and prompt patterns.
