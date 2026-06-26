# Индекс Wiki

> Каталог контента. Каждая wiki-страница перечислена в разделе своего типа с кратким описанием.
> Начинай отсюда, чтобы найти релевантные страницы для любого запроса.
> Последнее обновление: 2026-06-26 | Всего страниц: 24

## Сущности
<!-- Внутри раздела — по алфавиту -->
- [[ant-cli]] — CLI для Claude Platform: вызовы API-ресурсов, OAuth, shell/YAML workflows и управление Claude Managed Agents из Git/CI.
- [[claude-code]] — coding-agent CLI/TUI от Anthropic; Dynamic Workflows переносят оркестрацию субагентов в исполняемые скрипты со structured outputs.
- [[copilotkit]] — open-source frontend stack для AI-агентов: AG-UI, shared state, frontend tools, generative/headless UI, persistent threads и Inspector.
- [[fish-speech]] — open-source TTS/voice-cloning модель Fish Audio для локальной генерации речи, русского voice cloning и CLI-переозвучки видео.
- [[lift]] — open-source 9B vision-модель Datalab для извлечения структурированного JSON из PDF/изображений по JSON Schema.
- [[llm-checker]] — CLI-утилита для анализа локального железа и рекомендаций LLM под задачи вроде coding, reasoning и multimodal.
- [[opencode]] — open-source, provider-agnostic AI coding agent для автономной разработки через CLI/TUI.
- [[openai-codex-python-sdk]] — заявленный Python SDK для встраивания сессий Codex, шагов агента, потоковых обновлений, изображений и управления sandbox в Python-приложения.
- [[revealjs]] — открытый HTML-фреймворк для презентаций, полезный для поддерживаемых слайдов, сгенерированных с помощью AI.
- [[zvec]] — embedded/in-process vector database от Alibaba для локального similarity, full-text и hybrid search без отдельного сервера.

## Концепты
- [[agent-abstraction-levels]] — шкала уровней агентных систем от чата и скиллов до субагентов, agent teams и workflow с объяснением роста токенной стоимости.
- [[agent-looping]] — паттерн агентных циклов discovery → planning → execution → verification → iteration, включая single-agent loop, fleet loop, open looping и closed looping.
- [[ai-agent-orchestration]] — паттерн разделения AI-агентов на 24/7-оркестратора и специализированных исполнителей, чтобы закрывать рабочий цикл от задачи до следующего шага.
- [[agentic-coding-workflows]] — рабочие процессы агентов для разработки: инспекция кода, тесты, диагностика, исправления и контролируемая sandbox-автоматизация.
- [[agentic-frontend-stack]] — interface/protocol слой для agent-native приложений: AG-UI, shared state, frontend tools, human-in-the-loop, threads, inspector и generative UI.
- [[ai-engineering]] — интеграция AI-систем и AI-сгенерированных артефактов в поддерживаемые рабочие процессы разработки.
- [[ai-video-dubbing]] — workflow автоматической переозвучки видео: субтитры/ASR, локальная TTS, voice cloning, тайминги и сборка через ffmpeg.
- [[code-based-presentations]] — презентации, хранящиеся как текстовые или кодовые артефакты для Git, diff, автоматизации и публикации в вебе.
- [[codex-goal-mode]] — практики постановки измеримых целей для `/goal` в Codex: stop condition, быстрый feedback loop, чек-листы и Markdown-журналы.
- [[document-structured-extraction]] — schema-first workflow извлечения JSON/полей из PDF и изображений для автоматизации документных процессов.
- [[dynamic-workflows]] — скриптовая оркестрация агентных пайплайнов: промежуточные результаты живут в переменных скрипта, а шаги возвращают structured outputs.
- [[local-llm-hardware-fit]] — подбор локальных LLM под железо с учетом RAM/VRAM, backend, quantization, контекста и категории задачи.
- [[local-vector-search]] — паттерн локального/embedded similarity search для RAG, персональных knowledge base и edge-сценариев без отдельной vector DB инфраструктуры.

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
- [codex-goal-mode-measurable-goals-2026-06-14](raw/articles/codex-goal-mode-measurable-goals-2026-06-14.md) — статья о режиме `/goal` в Codex: измеримые цели, быстрые проверки и Markdown-файлы состояния для долгих агентных циклов.
- [copilotkit-frontend-stack-for-ai-agents-2026-05-20](raw/articles/copilotkit-frontend-stack-for-ai-agents-2026-05-20.md) — перевод статьи CopilotKit о frontend stack для AI-агентов: AG-UI, shared state, tools, persistent threads, generative UI, Inspector, MCP и self-improving agents.
- [opencode-ai-coding-agent-2026-06-03](raw/articles/opencode-ai-coding-agent-2026-06-03.md) — сохранённый ответ из диалога с кратким объяснением OpenCode как open-source AI coding agent для автономной разработки.
- [opencode-rules-agents-config-2026-06-05](raw/articles/opencode-rules-agents-config-2026-06-05.md) — сохранённая заметка о настройке поведения OpenCode через AGENTS.md, глобальные правила, opencode.json, agent-файлы и fallback на CLAUDE.md.
- [llm-checker-local-llm-recommendations-2026-06-02](raw/articles/llm-checker-local-llm-recommendations-2026-06-02.md) — пересланный пост об утилите llm-checker, которая анализирует железо и рекомендует локальные LLM под задачи вроде coding.
- [fish-speech-local-russian-voice-cloning-2026-06-14](raw/articles/fish-speech-local-russian-voice-cloning-2026-06-14.md) — заметка о Fish Speech как локальной open-source TTS/voice-cloning модели для русского языка и будущей CLI-переозвучки видео через Codex skill.
- [datalab-lift-document-structured-extraction-2026-06-20](raw/articles/datalab-lift-document-structured-extraction-2026-06-20.md) — пересланная заметка и видео о Lift, 9B open-source модели Datalab для structured extraction из документов по JSON Schema.
- [openai-codex-python-sdk-2026-06-02](raw/articles/openai-codex-python-sdk-2026-06-02.md) — пересланный пост с утверждением, что OpenAI выпустила Python SDK для Codex с сессиями, потоковыми обновлениями, изображениями и управлением sandbox.
- [revealjs-maintainable-ai-generated-presentations-2026-06-02](raw/articles/revealjs-maintainable-ai-generated-presentations-2026-06-02.md) — пересланный пост о том, почему Reveal.js лучше AI-инструментов дизайна для поддерживаемых презентаций.
- [agent-abstraction-levels-token-costs-2026-06-02](raw/articles/agent-abstraction-levels-token-costs-2026-06-02.md) — пересланный пост и схема о различиях между chat, skill, goal, subagent, agent team и workflow и о том, почему стоимость растет с координацией.
- [zvec-local-embedded-vector-search-2026-06-20](raw/articles/zvec-local-embedded-vector-search-2026-06-20.md) — пересланная заметка о zvec как локальной embedded vector database от Alibaba с full-text, hybrid search, DiskANN и Zvec Studio.
