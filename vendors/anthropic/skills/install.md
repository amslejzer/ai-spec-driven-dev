# Anthropic Skills: Installation

**Version:** 1.0
**Date:** 2026-04-24
**Status:** Vendor pack doc

How to install the Anthropic skills so they can be invoked from Claude Code in other projects.

## Scope

Claude Code loads slash commands from two locations:

- **User-level** — `~/.claude/commands/`. Available in every project on the machine.
- **Project-level** — `<project>/.claude/commands/`. Available only in that project. On name collision, project-level wins.

Choose user-level for cross-project use. Choose project-level to override a specific skill in a single project.

## The Dependency Problem

The skills are not fully self-contained. Several reference core repository files that do not travel with a simple `cp` of the skill markdown.

| Skill | External files read at runtime |
|---|---|
| `project-setup.md` | `templates/*.md` (all eight); `docs/pm-integration.md` |
| `ideation-partner.md` | `templates/ideation-notes-template.md` |
| `roadmap-planner.md` | `templates/roadmap-template.md`, `templates/task-template.md` |
| `implementation-planner.md` | `templates/implementation-plan-template.md` |
| `session-closer.md` | `templates/session-summary-template.md` |

All skills also use method vocabulary — phase names, role names, integration patterns, task ID scheme. Without access to a method primer, Claude must infer these from the skill body alone.

## Method Context Bundle

The recommended install pattern ships a small context bundle alongside the skills:

```
<bundle-root>/
  method-primer.md    ← condensed method context (shipped in this pack)
  templates/          ← copies of templates/ from the method repo
```

The primer is shipped at [method-primer.md](method-primer.md). It condenses `core-method.md`, `principles.md`, `glossary.md`, and the integration-pattern section of `pm-integration.md` into a single file the skills can `Read` at invocation time.

Once the bundle is in place, the skills are pointed at it by rewriting two relative paths per file.

## Install Recipes

### Recipe A: User-level bundled (recommended)

One copy of skills and the context bundle, available in every project.

```sh
REPO=/path/to/ai-spec-driven-dev
BUNDLE=~/.claude/ai-spec-method

mkdir -p ~/.claude/commands "$BUNDLE/templates"

# skills
cp "$REPO"/vendors/anthropic/skills/{project-setup,ideation-partner,roadmap-planner,implementation-planner,code-author,session-closer}.md \
   ~/.claude/commands/

# context bundle
cp "$REPO"/vendors/anthropic/skills/method-primer.md "$BUNDLE/"
cp "$REPO"/templates/*.md "$BUNDLE/templates/"

# rewrite references in installed skills
cd ~/.claude/commands
for f in *.md; do
  sed -i.bak \
    -e "s|templates/|$BUNDLE/templates/|g" \
    -e "s|docs/pm-integration.md|$BUNDLE/method-primer.md|g" \
    "$f"
  rm "$f.bak"
done
```

Optionally add a one-line preamble to each skill so the primer is loaded at the start of every invocation:

```
Read <BUNDLE>/method-primer.md for method context before starting.
```

- **Pros**: self-contained; works in every project; single source of truth at user level.
- **Cons**: upstream changes require re-sync.

### Recipe B: User-level repo-referenced

Skip the bundle. Have the skills reference the method repo at a fixed local path.

```sh
REPO=/path/to/ai-spec-driven-dev

cp "$REPO"/vendors/anthropic/skills/{project-setup,ideation-partner,roadmap-planner,implementation-planner,code-author,session-closer}.md \
   ~/.claude/commands/

cd ~/.claude/commands
for f in *.md; do
  sed -i.bak \
    -e "s|templates/|$REPO/templates/|g" \
    -e "s|docs/pm-integration.md|$REPO/docs/pm-integration.md|g" \
    "$f"
  rm "$f.bak"
done
```

- **Pros**: zero duplication; `git pull` in the method repo updates everything automatically.
- **Cons**: breaks if the repo moves or is absent on another machine; implicit dependency.

### Recipe C: Project-local

Install skills and templates into a single project. Fits the Repo-Canonical integration pattern: everything the project needs lives with the project.

```sh
REPO=/path/to/ai-spec-driven-dev
cd /path/to/project

mkdir -p .claude/commands templates
cp "$REPO"/vendors/anthropic/skills/{project-setup,ideation-partner,roadmap-planner,implementation-planner,code-author,session-closer}.md \
   .claude/commands/
cp "$REPO"/templates/*.md templates/
```

No rewrites needed — the skills' existing relative `templates/…` paths resolve from the project root at invocation time. The `docs/pm-integration.md` reference in `project-setup.md` will still fail unless the method primer or the `pm-integration.md` file itself is also copied in.

- **Pros**: fully portable per-project; no external dependencies once installed.
- **Cons**: repeated per project; template updates require per-project re-sync.

Note: `project-setup.md` is designed for an empty-or-near-empty folder. If `templates/` is pre-copied, the skill will prompt before continuing. That is expected behavior.

## Sync

Upstream changes to skills, the primer, or templates require re-syncing installed copies.

- **Recipe A**: re-run the `cp` commands. The `sed` rewrites only need to run on newly copied skill files.
- **Recipe B**: `git pull` in the method repo.
- **Recipe C**: re-run the `cp` commands in each project that needs the update.

## Adaptation

The install recipes preserve skill behavior verbatim. After install, a copy can be forked and adapted for a specific user or project. Once adapted, the adapted copy is canonical for that scope and upstream sync no longer applies to that file. See the adaptation note in [README.md](README.md).
