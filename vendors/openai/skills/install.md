# OpenAI Skills: Installation

**Version:** 1.0
**Date:** 2026-04-24
**Status:** Vendor pack doc

How to install the OpenAI role prompts into the surfaces where they will be used.

## Distribution Model

Unlike a Claude Code slash command file, the OpenAI role prompts are not file-based at the install target. They are blocks of instruction text designed to be pasted into a surface:

- ChatGPT project instructions
- Custom GPT instruction fields and knowledge files
- Codex CLI (`AGENTS.md` and, where supported, saved prompt files)
- Codex cloud (the ChatGPT-integrated coding agent) via committed `AGENTS.md`
- OpenAI API system prompts (production)

The role prompt content is the same; only its delivery target differs by surface.

## The Dependency Problem

The role prompts use method vocabulary — phase names, role names, integration patterns, artifact types, the task ID scheme. They reference repository artifacts (specs, task docs, plans) the user is expected to provide at session time, and they assume the surface AI can recognize what those artifacts are.

When a role prompt is pasted into a surface that has no access to the method repository — a fresh ChatGPT thread, a Custom GPT, or a Codex session in an unrelated project — the surface AI has only the prompt body to infer from.

The fix is the same as the Anthropic pack's: ship a method context primer and supply it alongside the role prompt. The primer is shipped at [method-primer.md](method-primer.md). It condenses `core-method.md`, `principles.md`, `glossary.md`, and the integration-pattern section of `pm-integration.md` into a single file the surface AI can read.

## Install Recipes

### Recipe A: ChatGPT project instructions

Use this when running a project's planning and documentation work inside a ChatGPT project workspace.

1. Create a ChatGPT project for the method project.
2. In the project Instructions field, paste the "Stable Project Context" template from [setup-context.md](../setup-context.md). Fill in the project-specific values.
3. Attach `method-primer.md` as a project file so it is available in every session inside this project.
4. Optionally attach the relevant template files from `templates/` as project files (e.g., `task-template.md`, `implementation-plan-template.md`).
5. For each working session, paste the relevant role's skill file as the first user message. Rotate roles by pasting a different skill at the start of the next session.

The project instructions become persistent stable context. Role prompts rotate per session. Use one role at a time.

### Recipe B: Custom GPT (one per role)

Use this when you want a reusable role configuration available across many projects, not tied to one workspace.

1. For each role, create a Custom GPT.
2. In the Instructions field, paste the contents of the role's skill file (e.g., `roadmap-planner.md`). Custom GPT instructions have a character limit, so keep this field focused on the role itself.
3. Upload `method-primer.md` to the GPT's Knowledge section so the model can retrieve method context as needed.
4. Upload the templates the role uses (e.g., `task-template.md` for the roadmap-planner GPT) to Knowledge.
5. Configure Capabilities the role actually needs. Most planning roles can run with browsing and code interpreter off.
6. Reuse the same Custom GPT across projects. Supply the project's specs and active task docs at session start.

### Recipe C: Codex CLI

Codex CLI is OpenAI's open-source command-line coding agent. It reads `AGENTS.md` files from the project tree as ambient instructions, and supports user-level configuration under `~/.codex/`.

Recommended setup:

1. **Method context** — paste the contents of `method-primer.md` into one of:
   - `~/.codex/AGENTS.md` for user-level scope (applies to every project Codex CLI touches on this machine), or
   - `<project>/AGENTS.md` for project-level scope (committed with the project).
   User-level is the better fit if you use the method across multiple projects; project-level is the better fit if the project is the only one using the method on this machine, or if teammates need the same context.
2. **Templates** — for project-level installs, commit the method's templates into the project (`templates/` at the project root) so the agent can read them by relative path during a session. For user-level installs, point Codex CLI at the method repo or copy the templates into a known local location and reference that path in `AGENTS.md`.
3. **Role prompts** — paste the role's skill file contents as the first message of the Codex CLI session. Codex CLI also supports saved/reusable prompt files; the directory and naming convention have evolved across releases, so check the current Codex CLI documentation for where to store role prompts as reusable commands. The skill file content drops in unchanged once the path is known.

### Recipe D: Codex cloud (ChatGPT-integrated coding agent)

Codex cloud is the ChatGPT-integrated coding agent that operates against a connected GitHub repository. It reads `AGENTS.md` from the repository.

1. Commit `AGENTS.md` at the project root. Include the project context (from `setup-context.md`'s Stable Project Context template) followed by the contents of `method-primer.md`, with clear section headings between them.
2. Commit `templates/` at the project root if the project follows the Repo-Canonical integration pattern. The agent will read templates by relative path when a role calls for them.
3. Paste the relevant role's skill file as the first message of the session.
4. Push `AGENTS.md` and `templates/` updates whenever the method or templates change upstream.

### Recipe E: API system prompts (production)

For production integrations using the OpenAI API directly, see [production-implementation.md](../production-implementation.md). In that pattern:

- the role prompt becomes the system prompt
- the method primer is part of the stable context layer (or accessed via a `get_document` tool call)
- templates and specs are fetched via tool calls rather than pasted into the prompt
- structured outputs are preferred over free-form prose for predictable artifacts

Do not attempt to build production tooling by repeatedly pasting the recipes above. The production pattern is meaningfully different.

## Sync

When upstream changes to the method, the primer, or the templates land in the method repository:

- **ChatGPT projects (Recipe A)** — re-paste updated content into the project Instructions field; re-upload changed files to project Files.
- **Custom GPTs (Recipe B)** — re-paste the role skill into Instructions if it changed; re-upload changed primer or templates to Knowledge.
- **Codex CLI (Recipe C)** — `git pull` in the method repo, then re-copy the primer text into your `AGENTS.md` (user-level or project-level). Re-copy templates if they changed.
- **Codex cloud (Recipe D)** — pull upstream changes, update the project's committed `AGENTS.md` and `templates/`, commit and push.
- **API (Recipe E)** — version your prompt and primer artifacts, and roll deploys per your normal process. Do not edit prompts in production without versioning.

## Adaptation

The role prompts are starting points, not frozen text. Once a role prompt is pasted into a Custom GPT, committed into a project's `AGENTS.md`, or shipped as part of an API system prompt, that copy is canonical for that scope and upstream sync no longer applies to it automatically. Adapt freely as real usage reveals gaps; treat the upstream version as a reference, not a constraint, after fork. See the adaptation note in [README.md](README.md).
