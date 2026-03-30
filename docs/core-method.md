# AI-Assisted Specification-Driven Development

**Version:** 1.1  
**Date:** 2026-03-30  
**Status:** Canonical core method

A vendor-neutral process for building complex projects with AI as a collaborator rather than treating AI as a code generator.

## Philosophy

"Vibe coding" implies improvisation. This method does the opposite: it front-loads thinking, treats documentation as a first-class deliverable, and uses AI as a thinking partner from ideation through implementation. Code is the last thing that gets written, and by the time it does, both the human and the AI should have enough context to build with intention.

## Core Principles

- **Plan heavy, code late.** Most of the leverage comes from ideation, specification, and implementation planning.
- **Documentation lives with the work.** Specs, plans, and task tracking belong in the repository with the codebase they describe.
- **AI changes roles, not ownership.** The human remains accountable for correctness and understanding while the AI changes behavior by task.
- **Markdown is the default medium.** It is simple, portable, human-readable, and easy for AI systems to produce and update.
- **Bookkeeping should be lightweight.** Session summaries, task updates, and other maintenance artifacts should be easy to keep current.
- **Every AI output must be reviewed.** Reading and understanding the artifacts is part of the method, not optional polish.

## The Process

### Phase 0: Project Setup

Initialize the repository before the project has code. Establish the documentation structure early so planning outputs are captured in version control from day one.

Typical outputs:

- repository initialized
- initial documentation folders created
- first commit made with structure in place

### Phase 1: Ideation

Use AI as a planning partner to stress-test the concept before design or implementation work starts. The goal is not to produce final artifacts immediately. The goal is to refine the idea until scope, constraints, and obvious risks are visible.

Typical outputs:

- refined problem statement
- intended audience and goals
- initial scope boundaries
- known risks and open questions

### Phase 2: Specification

Turn the project concept into formal documentation covering systems, architecture, workflows, interfaces, data, and constraints. This is where contradictions should be found and resolved before they become code.

Typical outputs:

- specification documents
- project documentation index
- clarified system boundaries
- initial AI context and instructions for future sessions

### Phase 3: Roadmapping

Break the specification into milestones, phases, and tasks. Tasks should be discrete, completable units of work with concrete checklists.

Typical outputs:

- milestone plan
- phased roadmap
- task definitions
- dependency-aware work ordering

### Phase 4: Implementation Loop

For each task, repeat the same cycle:

1. Plan the implementation from the task definition and relevant specs.
2. Build and test against explicit acceptance criteria.
3. Document the session and update the task state.
4. Feed discoveries back into future planning.

Typical outputs per cycle:

- implementation plan
- working tested changes
- updated task record
- session summary

### Phase 5: Maintenance

Once a project reaches a milestone or release state, continue using the same method for new work. Maintenance is not a lesser mode. It is the same specification-driven loop applied to an existing system.

Typical outputs:

- change specs
- updated roadmap items
- implementation plans for fixes or enhancements
- revised documentation reflecting current reality

## AI Roles in the Method

The method assumes AI takes on different roles across phases. The names and exact prompts can vary by vendor or tool, but the functional roles stay stable:

- ideation partner
- roadmap planner
- implementation planner
- code author
- session closer

These roles are part of the method. Specific skill files or prompt packs belong in vendor packs, not in the core method.

## What the Core Method Does Not Assume

The core method does not require:

- a specific AI vendor
- a specific editor or coding agent
- a specific repository layout beyond having a place for documentation
- a specific prompt format

Those choices can be layered on through optional vendor packs and project-specific adaptation.
