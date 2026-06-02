---
title: Code-Based Presentations
created: 2026-06-02
updated: 2026-06-02
type: concept
tags: [ai-engineering, workflow, devtools, architecture-pattern]
sources: [raw/articles/revealjs-maintainable-ai-generated-presentations-2026-06-02.md]
confidence: medium
---

# Code-Based Presentations

Code-based presentations are slide decks stored as normal text/code artifacts (for example HTML, Markdown, CSS, and JavaScript) rather than as opaque PowerPoint files or one-off AI design artifacts.

## Why it matters

For AI-assisted work, code-based decks make generated slides maintainable: changes can be reviewed with diffs, versioned in Git, edited in a code editor, templated, and deployed as a website. This aligns presentations with normal [[ai-engineering]] project workflows instead of separating them into external design tools.

## Practical pattern

A useful pattern is to ask an LLM such as Claude to generate a [[revealjs]] presentation using HTML/Markdown sources. The model can draft structure, content, and styling, while humans retain control over templates, animations, publication, and later edits.

## Benefits captured from the source

- Source files are text.
- The deck can live in Git.
- Developers can edit it in any code editor.
- Styles and animations are fully controllable.
- The presentation can be published as a normal website.
- The deck becomes part of the project rather than a standalone artifact living in PowerPoint or an AI design tool.

## Open questions

- When is a visual AI design tool still preferable to a code-based deck?
- What default Reveal.js template should be used for AI-generated project presentations?
- How should speaker notes and PDF export be standardized?

## Related

- [[revealjs]]
- [[ai-engineering]]
