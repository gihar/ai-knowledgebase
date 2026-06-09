---
title: Claude Code
created: 2026-06-09
updated: 2026-06-09
type: entity
tags: [claude, anthropic, coding-agent, cli, agent, workflow, devtools]
sources: [raw/articles/claude-code-dynamic-workflows-2026-06-09.md]
confidence: medium
---

# Claude Code

Claude Code — coding-agent CLI/TUI от Anthropic для работы с репозиториями, задачами разработки и агентными workflow. В базе знаний упоминается как один из исполнителей рядом с Codex, Cursor, Pi и [[opencode]] в паттерне [[ai-agent-orchestration]].

## Dynamic Workflows

Пересланная заметка фиксирует добавление Dynamic Workflows: механизма, где runtime выполняет скрипт, а не Claude turn-by-turn решает весь порядок работы. Скрипт может запускать субагентов, сохранять их результаты в переменных, требовать structured outputs и продолжать pipeline без загрузки всех промежуточных результатов в контекст Claude.

## Практическое значение

Для [[agentic-coding-workflows]] Claude Code Dynamic Workflows сдвигают фокус от «попросить агента сделать следующий шаг» к «описать исполняемый pipeline». Это ближе к [[dynamic-workflows]] и [[agent-looping]]: повторяемость находится в orchestration code, а не только в prompt или skill.

## Связанные страницы

- [[dynamic-workflows]]
- [[agentic-coding-workflows]]
- [[ai-agent-orchestration]]
- [[agent-looping]]
- [[opencode]]
