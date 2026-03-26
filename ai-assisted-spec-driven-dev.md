# AI-Assisted Specification-Driven Development

**Version:** 1.0  
**Date:** 2026-03-26  
**Author:** Andrew  
**AI Disclosure:** Drafted and refined with Claude (Anthropic). All ideas, process design, and editorial decisions are the author's.

A personal process guide for building complex projects with AI as a collaborator — not just a code generator.

---

## Philosophy

"Vibe coding" implies improvisation. This process is the opposite: it front-loads thinking, treats documentation as a first-class deliverable, and uses AI as a thinking partner from ideation through implementation. Code is the *last* thing that gets written, and by the time it does, the AI has deep context on what it's building and why.

The core principles:

- **Plan heavy, code late.** Most of the value comes from the specification and design phases. Code follows naturally from good specs.
- **Documentation lives with the code.** All specs, implementation docs, and project tracking live as markdown files in the repo. One source of truth, version-controlled alongside the codebase.
- **AI changes roles, not tools.** The same AI platform handles planning, documentation, implementation design, and code authoring — but with different skills (custom instructions) tuned for each role.
- **Markdown is the universal format.** It's human-readable, AI-readable, token-efficient, trivial for AI to write, and diffs cleanly in git.
- **Automate the bookkeeping.** Session summaries, task updates, and git commits happen through purpose-built skills so documentation stays current without manual effort.
- **Read everything the AI produces.** This is not a hands-off process. Every spec, every implementation doc, every piece of code the AI generates gets read, understood, and validated by a human before it moves forward. The AI is a collaborator, not an autopilot. Skipping this step is how "AI-assisted development" degrades back into vibe coding — you end up with a project you built but don't understand.

---

## Tooling

### Platform

- **Claude Projects** — Used for planning and ideation phases. Project-level context and instructions make it well-suited for long, iterative design conversations that span multiple chats.
- **Claude Code** — Used for building phases (implementation planning, code authoring, testing, session management). Its tighter skill customization and direct filesystem/git access make it the better fit for hands-on work. Increasingly considered for planning work as well, since skills can be more precisely tailored.

### Documentation Format

All project documentation is markdown, stored in the repository alongside the source code. This includes specs, implementation docs, the roadmap, task definitions, and session logs. The reasoning:

- Markdown is equally readable by humans and AI, with no parsing overhead.
- It's token-efficient — no markup bloat eating into context windows.
- AI can write and update it natively without tooling dependencies.
- It diffs cleanly in git, making documentation changes as trackable as code changes.
- It's portable — no vendor lock-in to any particular project management tool.

### Version Control

Git is used throughout the process, not just for code. Documentation changes, spec revisions, and implementation plans are all committed. Commits typically happen at the end of each working session, which in practice aligns with subtask completion. This gives a granular history of both the project's code and its evolving design.

---

## The Process

### Phase 0: Project Setup

Before anything else, initialize the project's git repository. Everything in this process — specs, implementation docs, roadmaps, task tracking, session logs, and eventually code — lives in the repo as markdown. Git is the backbone of the entire workflow, so it needs to exist from the start.

1. Create the repository (local and remote).
2. Establish an initial directory structure for documentation (e.g., `docs/`, `docs/specs/`, `docs/tasks/`).
3. Make an initial commit with the empty structure.

This also means the very first planning conversations can begin producing documentation that's immediately committed and tracked, rather than floating in chat history until "the code part" starts.

**Outputs:** An initialized git repository with a documentation directory structure, ready to receive project artifacts from the first planning session forward.

### Phase 1: Ideation

Every project starts with an idea — a game, a tool, a product, whatever it may be. The first step is standing up a new project in Claude and working through that idea conversationally.

This isn't a solo brainstorm dumped into a prompt. It's an iterative dialogue: describe the concept, let the AI push back, ask questions, surface edge cases, and identify potential issues. The goal is to stress-test the idea *before* any design or code work begins.

This phase can span multiple chat sessions depending on the project's complexity. Each session should have access to tools or connections that allow the conversation's output to be captured into formal documentation as the ideas solidify, rather than left stranded in chat history.

**Outputs:** A refined project concept with identified scope, core mechanics or features, and known risks or open questions — captured in documentation, not just chat logs.

### Phase 2: Specification

Once the idea is solid, it's time to formalize it. Working with AI, expand the concept into detailed specification documents covering the project's systems, architecture, data models, interactions, and constraints.

This is where the AI earns its keep as a design partner. It can help identify dependencies between systems, flag contradictions in the design, and flesh out details that are easy to overlook when designing alone. The specification process is iterative — write, review, revise, repeat.

Every spec document the AI produces needs to be genuinely read and understood, not just skimmed and approved. This is the design of the project — if something is wrong or unclear in the spec, it will compound through every downstream phase. The time spent carefully reading specs pays for itself many times over in avoided rework.

As the specification grows, two things need to happen in parallel:

- **Build the AI's project context.** Refine the project-level memory, instructions, and skills so that future sessions start with good context rather than requiring re-explanation.
- **Create a documentation index.** As docs multiply, maintain a table of contents or index file that future AI sessions can reference to locate the information they need. This becomes critical as the project scales — without it, the AI has to guess where things are or load everything at once.

**Outputs:** Formal specification documents, a documentation index, and a well-configured project with tuned instructions and skills.

### Phase 3: Roadmapping

With specifications complete, use the AI to plan a roadmap from the current state (zero) to defined milestones. Milestones might be a proof of concept, a tech demo, a feature-complete build, or a release — whatever makes sense for the project.

The roadmap breaks down into **phases**, and phases break down into **tasks**. Tasks are the atomic unit of the project management system — each one is a discrete, completable piece of work. So far, each task has included a checklist of specific items to accomplish.

The AI generates this roadmap using the spec docs as its source, which means the plan is grounded in the actual design rather than vague estimates.

**Outputs:** A phased roadmap with clearly defined milestones, phases, and tasks — each task with a checklist of concrete items.

### Phase 4: Implementation Loop (Plan → Build → Document → Repeat)

Phases 1–3 are sequential. Phase 4 is cyclical — it repeats for every task until the milestone is reached.

#### Step 1: Plan the Implementation

Before any code is written for a task, it goes through an implementation planning step. The task page is fed into an AI session equipped with a specific skill for this role. That skill instructs the AI to:

- Read and interpret the task definition
- Pull in relevant documentation from the spec (using the documentation index)
- Produce a detailed implementation document

Each implementation document includes:

- **Acceptance criteria** — Specific, testable conditions that define "done" for this task.
- **Test details** — What to test, how to test it, and expected outcomes.
- Additional context as needed (API contracts, data flow, edge cases, etc.)

This step bridges the gap between "what" (the spec) and "how" (the code). It gives the coding session a precise, unambiguous target to build toward. If a task is complex enough, the implementation plan may break it into subtasks, each with their own criteria.

Review the implementation document before moving to the build step. Verify that the acceptance criteria actually capture what "done" means for this task, that the test plan covers the right cases, and that the approach makes sense architecturally. This is the last checkpoint before code gets written — catching a bad assumption here is far cheaper than catching it in debugging.

#### Step 2: Build & Test

With the implementation document in hand, a new AI session is started with a skill specifically tuned for code authoring. This skill instructs the AI to:

- Read the implementation document
- Write the code to satisfy the acceptance criteria
- Run tests and validate against the defined test details

The build session is collaborative — work with the AI to debug, iterate, and refine until the acceptance criteria are met. The implementation doc serves as the contract: if the criteria pass, the task (or subtask) is done.

Read and understand the code as it's written. Don't just verify that tests pass — follow the logic, understand the patterns being used, and make sure the implementation makes sense to you. A passing test suite on code you don't understand is a liability, not an asset. The goal is a codebase you could maintain, debug, and extend yourself — the AI just helped you write it faster.

#### Step 3: Document & Close

At the end of each working session, a dedicated skill handles the wrap-up:

1. **Summarize the session** — Capture what was done, decisions made, and any issues encountered.
2. **Commit to git** — Stage and commit changes with a meaningful message reflecting the work completed.
3. **Update the task page** — Mark completed items, log what was accomplished, and record how long the session took.

This automated close-out keeps documentation current as a natural byproduct of the work rather than a separate maintenance chore.

#### Step 4: Feed Forward & Repeat

After a task is complete, loop back to Step 1 for the next task. Critically, any discoveries, design changes, or new context that emerged during the previous task carry forward into the next planning step. If building Task 1 revealed that a spec assumption was wrong or an interface needs to change, that information is available to the AI when planning Task 2's implementation.

This is where living documentation pays off — because specs and task pages are updated as part of the close-out step, the next planning session starts with an accurate picture of the project's current state.

The loop continues until all tasks in the current phase are complete and the milestone is reached.

**Outputs per cycle:** An implementation document, working tested code, updated task tracking, a git commit, and a session summary. **Outputs per milestone:** A complete, tested deliverable (proof of concept, tech demo, release, etc.) with full documentation of how it got there.

### Phase 5: Maintenance

Once a milestone is reached, the project enters a maintenance phase. The product is considered "complete" for the time being — but maintenance may look very similar to active development.

New features, bug fixes, design changes, and refinements all follow the same process: spec the change, roadmap it, plan the implementation, build, test, document. The only difference is the starting point — instead of building from zero, the project has an existing codebase, established documentation, and a history of decisions to build on.

The same skills, the same documentation practices, and the same cyclical implementation loop apply. Maintenance isn't a lesser phase — it's the same process with a different starting context.

**Outputs:** Continued evolution of the project following the same specification-driven workflow.

---

## Skills Reference

Skills are custom instruction sets that tell the AI how to behave in a specific role. They're the mechanism that lets a single AI platform handle fundamentally different jobs — planning vs. writing implementation docs vs. authoring code — without blurring responsibilities.

Each skill below is described by its purpose and expected behavior, not its literal prompt text. The intent is to be able to reconstruct and refine these skills over time rather than treat them as frozen artifacts.

### Ideation / Planning Partner

**Purpose:** Assist with brainstorming, concept refinement, and design exploration during the early phases.

**Behavior:** Engages conversationally with the project concept. Asks clarifying questions, identifies ambiguities, surfaces potential issues, and suggests alternatives. Pushes back constructively rather than just agreeing. Captures outputs into structured documentation as ideas solidify. Maintains awareness of the project's existing documentation to avoid contradictions.

### Roadmap Planner

**Purpose:** Transform completed specification documents into a structured, phased roadmap from the project's current state to defined milestones.

**Behavior:** Reads the full specification documentation using the project's documentation index. Identifies logical groupings of work and dependencies between systems. Proposes milestones that represent meaningful, demonstrable project states (proof of concept, tech demo, feature-complete, release). Breaks each milestone into phases, and phases into discrete tasks. Each task should include a checklist of concrete items to accomplish. Orders tasks to respect dependencies — foundational systems before features that rely on them. Flags any gaps or ambiguities in the specs that would block roadmap planning.

### Implementation Planner

**Purpose:** Transform a task definition into a detailed, actionable implementation document.

**Behavior:** Reads the task page and its checklist items. References relevant specification documents using the project's documentation index. Produces an implementation document containing acceptance criteria, test details, and any additional context needed for the build phase. Focuses on precision — the implementation doc should leave no ambiguity about what "done" looks like.

### Code Author

**Purpose:** Write and test code that satisfies an implementation document's acceptance criteria.

**Behavior:** Reads the implementation document as its primary input. Writes code targeting the defined acceptance criteria. Runs tests as specified in the test details. Iterates collaboratively through debugging until all criteria are met. Stays within the scope of the implementation doc — doesn't introduce unrequested features or architectural changes.

### Session Closer

**Purpose:** Automate end-of-session bookkeeping so documentation stays current without manual effort.

**Behavior:** Summarizes the work done during the session. Commits changes to git with a descriptive message. Updates the relevant task page with completed items and session duration. Designed to run at the natural end of a working session, typically aligned with subtask completion.

---

## Current State & Open Questions

This process is actively evolving. Areas still being refined:

- **Documentation templates** — The structure of spec docs, implementation docs, and task pages is not yet standardized into formal templates. Patterns are emerging from use but haven't been codified.
- **Planning tooling migration** — Currently using Claude Projects for planning and Claude Code for building. Moving planning into Claude Code (for tighter skill control) is under consideration.
- **Parallelism** — Tasks are currently handled sequentially. Exploring whether some tasks could be run in parallel once the process is more mature.
- **Skill refinement** — Skills are described functionally here and are expected to be iteratively rebuilt and improved as the process matures.
