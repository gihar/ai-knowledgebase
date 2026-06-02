# Wiki Schema

## Domain
AI knowledge base: artificial intelligence, machine learning, large language models, autonomous agents, AI engineering, evaluation, safety/alignment, inference, training, tooling, products, companies, labs, and practical implementation patterns.

## Conventions
- File names: lowercase, hyphens, no spaces (e.g., `transformer-architecture.md`).
- Every wiki page starts with YAML frontmatter.
- Use `[[wikilinks]]` to link between pages (minimum 2 outbound links per page where meaningful).
- When updating a page, always bump the `updated` date.
- Every new page must be added to `index.md` under the correct section.
- Every action must be appended to `log.md`.
- Raw sources in `raw/` are immutable: never rewrite source bodies after ingest; corrections go into Layer 2 wiki pages.
- Provenance markers: on pages synthesizing 3+ sources, append `^[raw/articles/source-file.md]` or `^[raw/papers/source-file.md]` after paragraphs whose claims trace to a specific source.
- Prefer concise, source-grounded synthesis over generic explanations.
- For fast-moving facts (model releases, benchmark scores, prices, API limits), mark confidence and include source dates.

## Frontmatter
```yaml
---
title: Page Title
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: entity | concept | comparison | query | summary
tags: [from taxonomy below]
sources: [raw/articles/source-name.md]
confidence: high | medium | low
contested: true
contradictions: [other-page-slug]
---
```

## raw/ Frontmatter
Raw sources must include:

```yaml
---
source_url: https://example.com/article
ingested: YYYY-MM-DD
sha256: <hex digest of the raw content below the frontmatter>
---
```

Compute SHA256 over the body only, not over the frontmatter.

## Tag Taxonomy
Use only tags listed here. Add new tags here before using them.

- Models and architectures: model, architecture, transformer, multimodal, reasoning, embedding, diffusion, speech, vision
- Training and data: training, fine-tuning, rlhf, dpo, grpo, data, synthetic-data, optimization, distributed-training
- Inference and deployment: inference, serving, quantization, caching, latency, gpu, edge, api, cost
- Evaluation: benchmark, eval, red-team, reliability, hallucination, observability
- Agents and tools: agent, tool-use, workflow, automation, mcp, rag, memory, planning
- Safety and governance: alignment, safety, security, privacy, policy, regulation, ethics
- Products and organizations: company, lab, open-source, product, platform, funding
- Software engineering: ai-engineering, architecture-pattern, prompt-engineering, testing, devtools
- Meta: comparison, timeline, controversy, prediction, glossary, query, summary

## Page Thresholds
- Create a page when an entity/concept appears in 2+ sources OR is central to one important source.
- Add to an existing page when a source mentions something already covered.
- Do not create pages for passing mentions, minor details, or items outside the AI domain.
- Split a page when it exceeds ~200 lines.
- Archive a page when its content is fully superseded: move it to `_archive/`, remove from index, and update backlinks.

## Entity Pages
One page per notable entity (model, company, lab, product, framework, dataset, benchmark, person if needed). Include:
- Overview / what it is
- Key facts and dates
- Relationships to other entities via `[[wikilinks]]`
- Source references
- Open questions / caveats for fast-moving claims

## Concept Pages
One page per concept or topic. Include:
- Definition / explanation
- Why it matters
- Current state of knowledge
- Practical implications
- Open questions or debates
- Related concepts via `[[wikilinks]]`

## Comparison Pages
Side-by-side analyses. Include:
- What is being compared and why
- Comparison dimensions (tables preferred in markdown)
- Verdict or synthesis
- Sources and confidence

## Query Pages
Use for valuable answers that would be painful to re-derive. Include:
- User question / research question
- Short answer
- Evidence and links to wiki pages
- Follow-up questions

## Update Policy
When new information conflicts with existing content:
1. Check source dates and publication context.
2. If newer data supersedes older data, preserve important historical context with dates.
3. If genuinely contradictory, note both positions with dates and sources.
4. Mark frontmatter with `contested: true` and/or `contradictions: [page-slug]`.
5. Flag unresolved contradictions in lint reports.
