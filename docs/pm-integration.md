# Project Management Integration

**Version:** 1.1
**Date:** 2026-03-31
**Status:** Supporting doc

The method includes a lightweight project management framework built on markdown files and version control. This document defines that framework explicitly and shows how it maps to external project management tools. No specific tool is required or assumed.

## The Markdown PM Framework

The method already organizes work into a three-level hierarchy. This section names that hierarchy as a PM framework and defines the conventions that make it function as one.

### Structure

Work is organized as:

- **Milestones**: meaningful project checkpoints with a demo or completion signal
- **Phases**: sequenced groups of related work within a milestone
- **Tasks**: the smallest planned unit of work, completable and reviewable independently

This hierarchy is defined in the roadmap and broken into individual task files.

### Tracking Surfaces

- A **roadmap file** (`docs/roadmap.md`) serves as the backlog and board view. It lists all milestones, phases, and tasks with their current status.
- **Task files** (`docs/tasks/`) hold the detail for each unit of work: goal, checklist, inputs, dependencies, and completion record.
- **Session summaries** serve as work logs, capturing what happened and what changed during a work session.

### Status Workflow

Each task carries a status in its `Status:` field. The default workflow is:

- `planned` — defined but not started
- `in-progress` — actively being worked
- `done` — completed and reviewed

Teams can extend this with values like `blocked` or `deferred` if needed. The important thing is that the set is documented for the project and used consistently.

### Conventions

- **Task IDs**: use a consistent scheme like `M1-P1-T1` (Milestone 1, Phase 1, Task 1) so tasks can be referenced unambiguously across files.
- **Status values**: pick a set and stick with it. Record the chosen values in the project's documentation index or roadmap header.
- **Cross-references**: roadmap entries should link to their task files. Task files should reference relevant specs and related tasks.

## Mapping to External PM Tools

The markdown framework maps to concepts found in most project management tools:

| Method Concept | PM Equivalent | Notes |
|---|---|---|
| Milestone | Epic | Meaningful checkpoint with completion signal |
| Phase | Sub-epic / Sprint grouping | Sequenced chunk within a milestone |
| Task | Story / Ticket / Issue | Smallest planned unit of work |
| Roadmap file | Backlog / Board | Aggregated view of all work and status |
| Task status | Workflow state | planned → in-progress → done |
| Implementation plan | Ticket description / AC | Detailed approach before work starts |
| Session summary | Work log / Comment | What happened and what changed |
| Task ID | Ticket number | Stable identifier for cross-referencing |

These mappings are approximate. The method does not require one-to-one correspondence. What matters is that the mapping is documented for the project and followed consistently.

## Integration Patterns

When connecting the markdown framework to an external PM tool, choose one of these patterns:

### Repo-Canonical (recommended default)

Markdown files in the repository are the source of truth. The PM tool mirrors them for visibility and team coordination. Task files are created in the repo first, then reflected in the PM tool. Status updates happen in the repo; the PM tool is updated to match.

Best for: solo work, small teams, projects where AI is the primary collaborator.
Trade-off: the PM tool may lag behind the repo. Requires discipline or light automation to keep current.

### PM-Canonical

The PM tool is the source of truth for planning and status. The repo holds implementation artifacts (implementation plans, session summaries, code) and links back to the PM tool using external IDs or URLs. Task detail lives in the PM tool; the repo references it.

Best for: teams where the PM tool is already the coordination surface and changing that is not realistic.
Trade-off: AI context loading is harder because the AI cannot read the PM tool directly. Relevant context may need to be copied into implementation plans.

### Hybrid

Planning artifacts exist in both places. The repo version is the detailed, AI-readable version. The PM tool version is the team-visible, workflow-tracked version. Links connect the two. Neither is strictly canonical — reconciliation happens at phase or milestone boundaries.

Best for: teams where both audiences (AI sessions and human coordination) are equally important.
Trade-off: more bookkeeping. Only justified when the coordination benefit is real.

## Keeping Sync Lightweight

Consistent with the principle that bookkeeping should be lightweight:

- Add an optional `External link:` field to task files when using an external tool. This is the bridge between systems.
- Sync PM tool status at session boundaries, not continuously. The session summary is the natural sync point.
- Use task IDs consistently across the repo and the PM tool so references stay unambiguous.
- Do not duplicate long-form content between systems. Link instead.
- Consider automation (scripts, webhooks, CI) only if manual sync becomes a genuine bottleneck.

## What the Framework Does Not Require

- A specific project management tool
- Sprints, story points, or velocity tracking
- A board view or kanban workflow
- Tool-specific automation or integration code

Teams may add any of these if they are useful. They are not part of the method. Tool-specific integration guidance could live in future integration packs outside the core documentation.
