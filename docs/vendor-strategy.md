# Vendor Strategy

**Version:** 1.2  
**Date:** 2026-04-24  
**Status:** Supporting doc

The core method is vendor-neutral. Vendor packs are optional extensions.

## What Belongs in the Core

Core documents should contain:

- the process itself
- role definitions at a functional level
- reusable templates
- repository conventions
- glossary and maintenance rules

Core documents should not contain:

- vendor-specific prompt text
- setup instructions for a specific platform
- assumptions about a specific coding agent
- platform-specific workflow mandates

## What Belongs in a Vendor Pack

Vendor packs may contain:

- setup and context guidance
- skill files or instruction folders
- prompt patterns
- tool-specific role mappings
- strengths, limitations, and caveats

## Design Rules for Vendor Packs

- Each vendor pack should stand on its own.
- Removing a vendor pack should not break the core documentation flow.
- Vendor packs should map to the core method rather than redefining it.
- New vendor packs should reuse the same high-level structure when possible.

## Standalone Dependencies

Vendor pack artifacts may reference core repository files such as templates, method docs, or glossary entries. Those references are real dependencies, not decoration.

When a vendor pack artifact is installed outside this repository — for example, a skill file copied into a user-level `.claude/commands/` directory — the referenced files do not travel with it. A vendor pack's install guidance must therefore specify:

- which of its artifacts depend on core repository files
- how those dependencies are expected to reach the install target (bundled copy, absolute path reference, project-local duplication, or similar)
- how to keep them synchronized with upstream changes

A vendor pack whose install guidance omits these points is not standalone in practice, even if it stands alone in structure.

## Current Default

The first concrete vendor pack in this repository is Anthropic because the method was initially exercised there. That is a practical starting point, not a statement that Anthropic is required by the method.
