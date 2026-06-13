# Индекс Wiki

> Каталог контента. Каждая wiki-страница перечислена в разделе своего типа с кратким описанием.
> Начинай отсюда, чтобы найти релевантные страницы для любого запроса.
> Последнее обновление: 2026-06-13 | Всего страниц: 15

## Сущности
<!-- Внутри раздела — по алфавиту -->
- [[ant-cli]] — CLI для Claude Platform: вызовы API-ресурсов, OAuth, shell/YAML workflows и управление Claude Managed Agents из Git/CI.
- [[claude-code]] — coding-agent CLI/TUI от Anthropic; Dynamic Workflows переносят оркестрацию субагентов в исполняемые скрипты со structured outputs.
- [[llm-checker]] — CLI-утилита для анализа локального железа и рекомендаций LLM под задачи вроде coding, reasoning и multimodal.
- [[opencode]] — open-source, provider-agnostic AI coding agent для автономной разработки через CLI/TUI.
- [[openai-codex-python-sdk]] — заявленный Python SDK для встраивания сессий Codex, шагов агента, потоковых обновлений, изображений и управления sandbox в Python-приложения.
- [[revealjs]] — открытый HTML-фреймворк для презентаций, полезный для поддерживаемых слайдов, сгенерированных с помощью AI.

## Концепты
- [[agent-abstraction-levels]] — шкала уровней агентных систем от чата и скиллов до субагентов, agent teams и workflow с объяснением роста токенной стоимости.
- [[agent-looping]] — паттерн агентных циклов discovery → planning → execution → verification → iteration, включая single-agent loop, fleet loop, open looping и closed looping.
- [[ai-agent-orchestration]] — паттерн разделения AI-агентов на 24/7-оркестратора и специализированных исполнителей, чтобы закрывать рабочий цикл от задачи до следующего шага.
- [[agentic-coding-workflows]] — рабочие процессы агентов для разработки: инспекция кода, тесты, диагностика, исправления и контролируемая sandbox-автоматизация.
- [[ai-engineering]] — интеграция AI-систем и AI-сгенерированных артефактов в поддерживаемые рабочие процессы разработки.
- [[code-based-presentations]] — презентации, хранящиеся как текстовые или кодовые артефакты для Git, diff, автоматизации и публикации в вебе.
- [[dynamic-workflows]] — скриптовая оркестрация агентных пайплайнов: промежуточные результаты живут в переменных скрипта, а шаги возвращают structured outputs.
- [[local-llm-hardware-fit]] — подбор локальных LLM под железо с учетом RAM/VRAM, backend, quantization, контекста и категории задачи.

## Сравнения
- [[claude-duet-vs-cowork]] — сравнение прямого режима Duet/Claude Code и Cowork через изолированную Linux VM: скорость и локальная интеграция против безопасности, чистого окружения и простого отката.

## Запросы

## Исходники
- [agent-looping-open-closed-fleet-2026-06-09](raw/articles/agent-looping-open-closed-fleet-2026-06-09.md) — пересланная заметка и схемы о single-agent/fleet agent looping, open/closed loops, стоимости и каталоге готовых loop-сценариев.
- [ai-agent-orchestration-vs-execution-2026-06-05](raw/articles/ai-agent-orchestration-vs-execution-2026-06-05.md) — пересланная заметка и схема о Hermes/OpenClaw как 24/7-оркестраторе и Codex/Claude Code/OpenCode как исполнителях.
- [anthropic-ant-cli-claude-platform-2026-06-03](raw/articles/anthropic-ant-cli-claude-platform-2026-06-03.md) — пересланный пост об ant CLI для Claude Platform, OAuth-авторизации, API-подкомандах и Claude Managed Agents.
- [claude-code-dynamic-workflows-2026-06-09](raw/articles/claude-code-dynamic-workflows-2026-06-09.md) — пересланная заметка и сравнительная схема о Claude Code Dynamic Workflows, subagents, skills, script variables и structured outputs.
- [claude-code-dynamic-workflows-official-docs-2026-06-09](raw/articles/claude-code-dynamic-workflows-official-docs-2026-06-09.md) — сохранённый ответ с деталями официальной документации Claude Code Dynamic Workflows: версии, `/deep-research`, `/effort ultracode`, `/workflows`, save locations, args, limits и permissions.
- [claude-duet-vs-cowork-sandbox-2026-06-13](raw/articles/claude-duet-vs-cowork-sandbox-2026-06-13.md) — пересланная схема о различиях Duet/Claude Code с прямым доступом к проекту и Cowork, который выполняет задачу в изолированной Linux VM-песочнице.
- [opencode-ai-coding-agent-2026-06-03](raw/articles/opencode-ai-coding-agent-2026-06-03.md) — сохранённый ответ из диалога с кратким объяснением OpenCode как open-source AI coding agent для автономной разработки.
- [opencode-rules-agents-config-2026-06-05](raw/articles/opencode-rules-agents-config-2026-06-05.md) — сохранённая заметка о настройке поведения OpenCode через AGENTS.md, глобальные правила, opencode.json, agent-файлы и fallback на CLAUDE.md.
- [llm-checker-local-llm-recommendations-2026-06-02](raw/articles/llm-checker-local-llm-recommendations-2026-06-02.md) — пересланный пост об утилите llm-checker, которая анализирует железо и рекомендует локальные LLM под задачи вроде coding.
- [openai-codex-python-sdk-2026-06-02](raw/articles/openai-codex-python-sdk-2026-06-02.md) — пересланный пост с утверждением, что OpenAI выпустила Python SDK для Codex с сессиями, потоковыми обновлениями, изображениями и управлением sandbox.
- [revealjs-maintainable-ai-generated-presentations-2026-06-02](raw/articles/revealjs-maintainable-ai-generated-presentations-2026-06-02.md) — пересланный пост о том, почему Reveal.js лучше AI-инструментов дизайна для поддерживаемых презентаций.
- [agent-abstraction-levels-token-costs-2026-06-02](raw/articles/agent-abstraction-levels-token-costs-2026-06-02.md) — пересланный пост и схема о различиях между chat, skill, goal, subagent, agent team и workflow и о том, почему стоимость растет с координацией.
