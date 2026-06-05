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


## [2026-06-02] ingest | llm-checker local LLM recommendations
- Captured forwarded post as `raw/articles/llm-checker-local-llm-recommendations-2026-06-02.md`.
- Copied screenshot asset to `raw/assets/llm-checker-recommend-coding-screenshot-2026-06-02.jpg`.
- Created `entities/llm-checker.md`.
- Created `concepts/local-llm-hardware-fit.md`.
- Updated `concepts/ai-engineering.md` with local-model hardware fit pattern.
- Updated `index.md`.

## [2026-06-02] ingest | Agent abstraction levels and token costs
- Captured forwarded post as `raw/articles/agent-abstraction-levels-token-costs-2026-06-02.md`.
- Copied screenshot asset to `raw/assets/agent-abstraction-levels-token-costs-2026-06-02.jpg`.
- Created `concepts/agent-abstraction-levels.md`.
- Updated `concepts/ai-engineering.md` with the agent-level scaling pattern.
- Updated `concepts/agentic-coding-workflows.md` with a link to agent abstraction levels.
- Updated `index.md`.


## [2026-06-03] ingest | OpenCode AI coding agent
- Captured conversation answer as `raw/articles/opencode-ai-coding-agent-2026-06-03.md`.
- Created `entities/opencode.md`.
- Updated `concepts/agentic-coding-workflows.md` with CLI/TUI coding agent pattern.
- Updated `concepts/ai-engineering.md` with OpenCode as developer workflow tooling.
- Updated `index.md`.


## [2026-06-03] ingest | Anthropic ant CLI for Claude Platform
- Captured forwarded post as `raw/articles/anthropic-ant-cli-claude-platform-2026-06-03.md`.
- Copied screenshot asset to `raw/assets/ant-cli-auth-login-2026-06-03.jpg`.
- Created `entities/ant-cli.md`.
- Updated `concepts/agentic-coding-workflows.md` with API-first CLI / Managed Agents pattern.
- Updated `concepts/ai-engineering.md` with Claude Platform CLI bridge pattern.
- Updated `index.md`.

## [2026-06-05] ingest | OpenCode rules and agents config
- Captured Telegram note as `raw/articles/opencode-rules-agents-config-2026-06-05.md`.
- Updated `entities/opencode.md` with AGENTS.md, `opencode.json`, custom agents, prompt-file and Claude fallback notes.
- Updated `concepts/agentic-coding-workflows.md` with project rules as part of the agent workflow.
- Updated `concepts/ai-engineering.md` with reproducible coding-agent instruction artifacts.
- Updated `index.md`.
