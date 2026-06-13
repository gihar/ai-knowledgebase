---
title: Claude Code
created: 2026-06-09
updated: 2026-06-13
type: entity
tags: [claude, anthropic, coding-agent, cli, agent, workflow, devtools]
sources: [raw/articles/claude-code-dynamic-workflows-2026-06-09.md, raw/articles/claude-code-dynamic-workflows-official-docs-2026-06-09.md, raw/articles/claude-duet-vs-cowork-sandbox-2026-06-13.md]
confidence: medium
---

# Claude Code

Claude Code — coding-agent CLI/TUI от Anthropic для работы с репозиториями, задачами разработки и агентными workflow. В базе знаний упоминается как один из исполнителей рядом с Codex, Cursor, Pi и [[opencode]] в паттерне [[ai-agent-orchestration]].

## Dynamic Workflows

Пересланная заметка фиксирует добавление Dynamic Workflows: механизма, где runtime выполняет скрипт, а не Claude turn-by-turn решает весь порядок работы. Скрипт может запускать субагентов, сохранять их результаты в переменных, требовать structured outputs и продолжать pipeline без загрузки всех промежуточных результатов в контекст Claude.

По официальной документации Claude Code Dynamic Workflows требуют версии v2.1.154+ и доступны на paid plans, через Anthropic API access, Amazon Bedrock, Google Cloud Vertex AI и Microsoft Foundry. На Pro включаются через `/config`. Built-in пример — `/deep-research <question>`, а custom workflows запускаются просьбой “use/run a workflow”, keyword `ultracode` или режимом `/effort ultracode`.

## Практическое значение

Для [[agentic-coding-workflows]] Claude Code Dynamic Workflows сдвигают фокус от «попросить агента сделать следующий шаг» к «описать исполняемый pipeline». Это ближе к [[dynamic-workflows]] и [[agent-looping]]: повторяемость находится в orchestration code, а не только в prompt или skill.

Практически это делает Claude Code пригодным для codebase-wide audits, крупных миграций, multi-agent QA и deep research, но переносит риски в cost/rate limits, permissions, качество aggregation и тестирование самого workflow script.

## Duet и Cowork как разные границы доступа

Схема [[claude-duet-vs-cowork]] добавляет важное различие между прямым режимом Duet/Claude Code и Cowork через изолированную VM. В обоих случаях Claude проходит похожий цикл разработки — понимает задачу, читает код, меняет файлы, ставит зависимости и запускает тесты. Разница в том, где выполняются команды: Duet работает непосредственно с локальным проектом и ОС пользователя, а Cowork копирует проект в Linux VM-песочницу и возвращает только изменённые файлы и логи.

Практически это делает Duet быстрее и удобнее для разработчиков, но рискованнее по правам доступа; Cowork медленнее и дороже по накладным расходам, зато лучше изолирует вредоносный код, зависимости и сбои окружения.

## Связанные страницы

- [[dynamic-workflows]]
- [[agentic-coding-workflows]]
- [[claude-duet-vs-cowork]]
- [[ai-agent-orchestration]]
- [[agent-looping]]
- [[opencode]]
