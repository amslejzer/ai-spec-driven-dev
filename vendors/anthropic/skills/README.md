# Anthropic Skills

**Version:** 1.3
**Date:** 2026-04-24
**Status:** Vendor pack doc

These are Claude Code skill files, intended to be installed into a `.claude/commands/` directory and invoked as slash commands.

## Installation

See [install.md](install.md) for the full install guide, including scope choices (user-level vs. project-level), the method context bundle, and three install recipes with trade-offs.

Once installed, the skills are invoked as:

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

## Included Context

| File | Purpose |
|---|---|
| [install.md](install.md) | Installation guide and recipes |
| [method-primer.md](method-primer.md) | Condensed method context shipped alongside installed skills |

## Adaptation

These skills are starting points. Adapt them as real usage reveals gaps or unnecessary detail. The behavioral instructions in each skill are drawn from the methodology's core principles and prompt patterns.
