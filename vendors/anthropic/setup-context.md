# Setup and Context Guidance

**Version:** 1.1  
**Date:** 2026-03-30  
**Status:** Vendor pack doc

Use this document when applying the method in Anthropic-oriented environments.

## Recommended Context Layers

- project summary
- current milestone or active task
- documentation index
- relevant specs
- any role-specific skill or instructions

## Practical Guidance

- Keep long-lived project context short enough to stay maintainable.
- Prefer linking or referencing canonical docs instead of repeating them in every session.
- Refresh the active task context at the start of a build session.
- Separate planning context from implementation context when possible so the AI role stays clear.

## Good Fit Areas

- long planning conversations
- iterative document refinement
- role-specific instruction sets

## Watchouts

- context drift when too many docs are loaded at once
- blurred role boundaries when one session tries to ideate, spec, implement, and close all at once
- over-trusting polished prose without reviewing the logic
