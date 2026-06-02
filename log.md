# Wiki Log

> Chronological record of all wiki actions. Append-only.
> Format: `## [YYYY-MM-DD] action | subject`
> Actions: ingest, update, query, lint, create, archive, delete
> When this file exceeds 500 entries, rotate: rename to `log-YYYY.md`, start fresh.

## [2026-06-02] create | Wiki initialized
- Domain: AI knowledge base — AI/ML, LLMs, agents, AI engineering, evals, safety, tools, companies, and practical implementation patterns.
- Structure created with SCHEMA.md, index.md, log.md, raw/, entities/, concepts/, comparisons/, queries/, _meta/.
- Path: /home/user/ai-knowledgebase

## [2026-06-02] ingest | Reveal.js for maintainable AI-generated presentations
- Captured forwarded post as `raw/articles/revealjs-maintainable-ai-generated-presentations-2026-06-02.md`.
- Copied image asset to `raw/assets/revealjs-readme-screenshot-2026-06-02.jpg` if available.
- Created `concepts/code-based-presentations.md`.
- Created `entities/revealjs.md`.
- Created `concepts/ai-engineering.md`.
- Updated `index.md`.

## [2026-06-02] ingest | OpenAI Codex Python SDK forwarded post
- Captured forwarded post as `raw/articles/openai-codex-python-sdk-2026-06-02.md`.
- Copied screenshot asset to `raw/assets/openai-codex-python-sdk-example-2026-06-02.jpg` if available.
- Created `entities/openai-codex-python-sdk.md`.
- Created `concepts/agentic-coding-workflows.md`.
- Updated `concepts/ai-engineering.md` with embedded coding-agent pattern.
- Updated `index.md`.

## [2026-06-02] update | Russian article content rule
- Проверены текущие wiki-страницы и описания в `index.md` на соответствие правилу русского контента.
- Переведены содержательные описания в `entities/`, `concepts/` и `index.md` на русский язык с сохранением имен технологий, команд, кода и wiki-ссылок.
- Переведены служебные подписи в `raw/articles/`; исходный текст постов и код сохранены, `sha256` пересчитан по обновленному телу файлов.

## [2026-06-02] update | Image embeds in raw articles
- Добавлено правило: изображения источников сохраняются в `raw/assets/` и вставляются в `raw/articles/` через Markdown image embed.
- В `raw/articles/openai-codex-python-sdk-2026-06-02.md` вставлена картинка `../assets/openai-codex-python-sdk-example-2026-06-02.jpg`.
- В `raw/articles/revealjs-maintainable-ai-generated-presentations-2026-06-02.md` вставлена картинка `../assets/revealjs-readme-screenshot-2026-06-02.jpg`.
- `sha256` обоих raw-файлов пересчитан по обновленному телу.

## [2026-06-02] update | Git synchronization rule
- Added SCHEMA.md rule: always run `git pull --ff-only` before any work with the base.
- Added SCHEMA.md rule: after changes, commit and `git push` to `origin/main`.
