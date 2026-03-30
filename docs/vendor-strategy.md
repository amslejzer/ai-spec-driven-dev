# Vendor Strategy

**Version:** 1.1  
**Date:** 2026-03-30  
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

## Current Default

The first concrete vendor pack in this repository is Anthropic because the method was initially exercised there. That is a practical starting point, not a statement that Anthropic is required by the method.
