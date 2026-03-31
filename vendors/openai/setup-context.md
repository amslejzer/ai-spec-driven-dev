# Setup and Context Guidance

**Version:** 1.0
**Date:** 2026-03-31
**Status:** Vendor pack doc

Use this document when applying the method in OpenAI-oriented environments.

## Recommended Context Layers

- project summary
- current milestone or active task
- documentation index
- relevant specs
- any role-specific skill or instructions

These map naturally to OpenAI features: custom instructions for persistent context, system prompts in API calls for role-specific behavior, GPT configurations for bundling a skill with its context, and project-level instructions in ChatGPT Projects for scoping context to a specific effort.

## Practical Guidance

- Use custom instructions for stable project-level context that should carry across ChatGPT sessions.
- Use project-level instructions in ChatGPT Projects to scope context to a specific initiative or phase.
- Use GPT configurations to bundle a role skill with relevant context into a reusable tool.
- Use system prompts in API calls to set role-specific behavior programmatically.
- Refresh the active task context at the start of a build session.
- Separate planning context from implementation context when possible so the AI role stays clear.

## Good Fit Areas

- long planning conversations
- iterative document refinement via canvas
- role-specific instruction sets via GPTs or system prompts

## Watchouts

- custom instructions have strict character limits — prioritize the most impactful context
- context drift when too many documents are attached or pasted at once
- blurred role boundaries when one session tries to ideate, spec, implement, and close all at once
- canvas edits can diverge from chat context if not reconciled
- over-trusting polished prose without reviewing the logic
