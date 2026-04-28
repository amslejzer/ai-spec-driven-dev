# AI-Assisted Specification-Driven Development: Method Primer

**Version:** 1.0
**Date:** 2026-04-24
**Status:** Vendor pack context artifact

This primer condenses the method for use as runtime context by vendor pack skills. It is not the canonical method doc — see the `ai-spec-driven-dev` repository for the full version (`docs/core-method.md`, `docs/principles.md`, `docs/pm-integration.md`, `docs/glossary.md`).

## What the Method Is

A vendor-neutral process for building projects with AI as a collaborator. It front-loads thinking: ideation, specification, and planning precede code. Documentation lives with the work in the repository. AI changes roles by phase; humans remain accountable for correctness.

## Principles

- **Plan heavy, code late.** Most leverage comes from planning, not generation.
- **Documentation lives with the work.** Specs, plans, and tasks belong in the repo.
- **AI changes roles, not ownership.** Humans own correctness and understanding.
- **Markdown is the default medium.** Portable, reviewable, easy for AI to update.
- **Bookkeeping should be lightweight.** Sessions and tasks stay cheap to maintain.
- **Every AI output must be reviewed.** Review is method, not polish.

## Phases

0. **Project Setup** — initialize the repo and scaffold documentation before any code.
1. **Ideation** — refine the concept; surface scope, constraints, and risks.
2. **Specification** — formalize systems, architecture, data, and interfaces.
3. **Roadmapping** — break specs into milestones, phases, and tasks.
4. **Implementation Loop** — per task: plan → build → test → document → update.
5. **Maintenance** — same loop, applied to existing systems.

## AI Roles

Each functional role corresponds to a skill in this vendor pack:

| Phase | Role | Skill |
|---|---|---|
| 0 | project setup | project-setup |
| 1 | ideation partner | ideation-partner |
| 3 | roadmap planner | roadmap-planner |
| 4 (plan) | implementation planner | implementation-planner |
| 4 (build) | code author | code-author |
| any | session closer | session-closer |

## Integration Patterns

Projects choose one at setup; the choice is captured in `docs/project-bootstrap.md`.

- **Repo-Canonical (default)** — all method artifacts (specs, plans, tasks, sessions) live in the repository. External PM tools are optional mirrors.
- **PM-Canonical** — an external PM tool (Jira, Linear, Notion, etc.) owns task records. The repo still holds specs and plans; tasks are referenced by external ID.
- **Hybrid** — specs and plans in the repo; tasks split between repo and external tool. An explicit convention declares which artifacts live where.

## Task ID Scheme

Default `M1-P1-T1` — milestone, phase, task. Tasks are discrete, completable units with acceptance criteria. Default status workflow: `planned → in-progress → done`.

## Artifact Types

- **Spec** — formal description of a system, feature, or change. `docs/specs/`.
- **Task** — completable unit of work with checklist, acceptance, and status. `docs/tasks/` (or external PM tool).
- **Plan** — implementation plan for a specific task. `docs/plans/`.
- **Session Summary** — record of what was done in a work session. `docs/sessions/`.
- **Ideation Notes** — pre-spec refinement. `docs/ideation-notes.md`.
- **Bootstrap** — project metadata captured at setup. `docs/project-bootstrap.md`.
- **Documentation Index** — map of project documentation. `docs/index.md`.

## Glossary

- **Method** — the process described in this primer.
- **Vendor pack** — an optional extension that maps the method to a specific AI platform (e.g., Anthropic, OpenAI).
- **Skill** — an instruction artifact for a single AI role in a specific tool context.
- **Canonical artifact** — the authoritative version of a piece of information. The method deliberately chooses a canonical location (repo vs. PM tool) for each artifact type.
