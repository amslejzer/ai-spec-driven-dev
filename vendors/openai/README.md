# OpenAI Vendor Pack

**Version:** 1.1
**Date:** 2026-03-31
**Status:** Vendor pack

This pack maps the core method to OpenAI-oriented workflows and artifacts.

It is optional. The methodology does not require OpenAI tools. This pack exists to help practitioners apply the method using OpenAI's ecosystem without rewriting the method itself.

## Included Resources

- [Setup and Context Guidance](setup-context.md)
- [Role Mapping](role-mapping.md)
- [Prompt Patterns](prompt-patterns.md)
- [Production Implementation Guide](production-implementation.md)
- [Skills](skills/README.md)

## Quick Start

If you want the shortest path from this repository to a working OpenAI setup:

1. Read [setup-context.md](setup-context.md) and choose where each layer of context will live.
2. Read [role-mapping.md](role-mapping.md) to decide which OpenAI surface each role should use.
3. Copy a prompt from [prompt-patterns.md](prompt-patterns.md) or a role prompt from [skills/README.md](skills/README.md).
4. If you are building a production integration, implement the workflow in [production-implementation.md](production-implementation.md).

## Best Fit

Use this pack when:

- you are planning or building with OpenAI-oriented tools such as ChatGPT, Codex, or the OpenAI API
- you want copy-paste starter prompts for the major method roles
- you want production guidance for implementing role prompts with tool calling and repository-aware workflows

## Copy-Paste Targets

This pack is written so the same role instructions can be reused in several places:

- ChatGPT project instructions for project-scoped planning and documentation work
- Custom GPT instructions for reusable planning roles
- Codex or repository-connected coding agents for implementation work
- OpenAI API system prompts for production applications and internal tools

Each document calls out where the content is best pasted.

## What This Pack Does Not Change

- the phases of the core method
- the expectation that humans review AI outputs
- the use of templates and examples as optional supports
- the requirement to keep documentation and task state in the repository
