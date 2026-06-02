---
title: AI Engineering
created: 2026-06-02
updated: 2026-06-02
type: concept
tags: [ai-engineering, workflow, devtools, automation]
sources: [raw/articles/revealjs-maintainable-ai-generated-presentations-2026-06-02.md, raw/articles/openai-codex-python-sdk-2026-06-02.md]
confidence: medium
---

# AI Engineering

AI engineering is the practice of integrating AI systems and AI-generated artifacts into maintainable software workflows.

## Example: presentations as project artifacts

The Reveal.js presentation workflow is a small but concrete example of AI engineering: instead of asking an AI design tool to produce a standalone deck, the user asks an LLM to generate source-controlled HTML/Markdown slides. This makes the output reviewable, editable, automatable, and publishable like normal code.

## Example: embedded coding agents

The forwarded post about [[openai-codex-python-sdk]] describes a possible shift from invoking a coding agent through CLI wrappers to embedding Codex sessions directly inside Python applications. That pattern fits [[agentic-coding-workflows]] because the surrounding product can manage sessions, streaming updates, images, and sandbox permissions as part of normal application logic.

## Related

- [[agentic-coding-workflows]]
- [[code-based-presentations]]
- [[openai-codex-python-sdk]]
- [[revealjs]]
