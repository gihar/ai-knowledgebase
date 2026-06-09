---
title: Dynamic workflows
type: concept
created: 2026-06-09
updated: 2026-06-09
tags: [agent, workflow, automation, coding-agent, structured-output, orchestration, claude-code, ai-engineering]
sources: [raw/articles/claude-code-dynamic-workflows-2026-06-09.md, raw/articles/claude-code-dynamic-workflows-official-docs-2026-06-09.md]
confidence: medium
---

# Dynamic workflows

Dynamic workflows — паттерн управления агентными пайплайнами, где очередность шагов, запуск субагентов, structured outputs и хранение промежуточных результатов контролируются скриптом, а не основным агентом-оркестратором в его контекстном окне.

## Ключевая идея

В классическом режиме основной агент вызывает субагентов и получает их результаты обратно в свой контекст. Это удобно для нескольких задач, но плохо масштабируется: промежуточные выводы съедают context window, а каждый следующий шаг выбирается моделью turn-by-turn.

В dynamic workflow управляющая логика становится исполняемым скриптом. Скрипт решает, какой шаг запустить дальше, какие данные передать модели, где сохранить результаты и какие проверки выполнить перед продолжением. Промежуточные результаты живут в переменных или структурах данных скрипта, поэтому не обязаны попадать целиком в контекст LLM.

## Официальная механика Claude Code

Официальная документация Claude Code описывает workflow как JavaScript-скрипт, который Claude пишет под задачу, а runtime исполняет в фоне отдельно от текущего диалога. Требуется Claude Code v2.1.154+. В Claude Code уже есть bundled workflow `/deep-research <question>`, который запускает web search по нескольким углам, fetch/cross-check источников, голосование по claims и возвращает cited report с отфильтрованными неподтверждёнными claims.

Свой workflow можно запустить прямой просьбой “use/run a workflow” или ключевым словом `ultracode`. Режим `/effort ultracode` включает xhigh reasoning effort и автоматическую workflow orchestration для substantive tasks; один запрос может стать несколькими workflows подряд: понять код, внести изменение, проверить результат.

## Отличие от subagents и skills

- **Subagents** масштабируют работу за счет отдельных worker-сессий, но управление и промежуточные результаты часто возвращаются в контекст основного агента.
- **Skills** делают поведение повторяемее через инструкции, но не переносят оркестрацию в исполняемый код.
- **Workflows** делают повторяемой саму оркестрацию: порядок шагов, условия ветвления, формат ответов, ретраи, агрегацию и точку остановки.

## Почему это важно

Dynamic workflows уменьшают «налог на контекст»: десятки или сотни субагентов можно запускать в одном run, если их полные ответы не нужно держать в рабочем контексте Claude. Для [[agent-looping]] это практический вариант closed loop: человек заранее проектирует скриптовой каркас, а модель работает внутри шагов с заданным structured output.

## Structured outputs

Structured outputs позволяют каждому шагу возвращать ответ в заранее заданном формате: JSON, typed schema или другой валидируемый контракт. Это превращает LLM-ответ из текста для чтения человеком в данные для следующего шага pipeline.

## Операционные детали

- `/workflows` показывает running/completed workflows, phases, agent count, token total и elapsed time.
- Workflow можно сохранить как slash-command в `.claude/workflows/` внутри проекта или `~/.claude/workflows/` глобально; project workflow побеждает personal workflow при конфликте имён.
- Saved workflow принимает structured `args`, доступные скрипту как глобальная переменная.
- Каждый run пишет script под `~/.claude/projects/`; его можно открыть, diff’нуть, отредактировать и попросить Claude перезапустить.
- Resume работает в пределах той же Claude Code session: завершённые agents возвращаются из cache, остальные запускаются live.
- Сам workflow script не имеет прямого shell/filesystem access; он координирует agents, а agents читают/пишут файлы и запускают команды.
- Лимиты: до 16 concurrent agents и до 1000 agents per run.
- Spawned subagents работают в `acceptEdits` и наследуют tool allowlist; file edits auto-approved, но shell/web/MCP tools вне allowlist могут запросить permission mid-run.

## Практические применения

- deep research: массовый сбор источников, извлечение фактов, дедупликация и финальный синтез;
- codebase analysis: параллельный обход модулей, сбор findings и агрегированный report;
- migration planning: разбиение большого проекта на независимые checks и последующее объединение плана;
- QA/review: запуск множества специализированных reviewer-субагентов с единым schema для findings;
- документирование: параллельный сбор контекста и генерация структурированных разделов.

## Риски и ограничения

- Скриптовая оркестрация становится production-кодом: её нужно тестировать, версионировать и логировать.
- Structured output снижает хаос, но не гарантирует истинность результата; внешняя проверка всё равно нужна.
- Масштаб «100 субагентов» переносит проблему из context window в стоимость, latency, rate limits и качество агрегации.
- Слишком жесткий workflow может пропустить неожиданные гипотезы, которые нашёл бы open loop.

## Связанные страницы

- [[claude-code]]
- [[agent-looping]]
- [[agentic-coding-workflows]]
- [[agent-abstraction-levels]]
- [[ai-engineering]]
