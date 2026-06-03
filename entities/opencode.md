---
title: OpenCode
created: 2026-06-03
updated: 2026-06-03
type: entity
tags: [agent, devtools, open-source, ai-engineering, automation]
sources: [raw/articles/opencode-ai-coding-agent-2026-06-03.md]
confidence: medium
---

# OpenCode

OpenCode — open-source AI coding agent для автономной работы с кодом через CLI/TUI. По роли он похож на Claude Code или Codex CLI, но важная особенность — провайдер-независимость: инструмент можно подключать к разным LLM-провайдерам и моделям.

## Ключевые возможности

- запуск одноразовых задач через `opencode run "..."`;
- интерактивная работа в терминальном TUI;
- чтение проекта, редактирование файлов и запуск команд в рабочей директории;
- типовые задачи: исправление багов, добавление фич, рефакторинг, написание тестов и ревью PR;
- параллельное выполнение задач в отдельных workdir или git worktree, чтобы избежать конфликтов.

## Примеры команд

```bash
opencode run "Добавь retry logic для API-запросов и обнови тесты"
opencode pr 42
```

Установка обычно выполняется через npm или Homebrew:

```bash
npm i -g opencode-ai@latest
brew install anomalyco/tap/opencode
```

После установки нужно настроить авторизацию, например через:

```bash
opencode auth login
```

## Практический смысл

OpenCode относится к [[agentic-coding-workflows]]: разработчик формулирует проверяемую задачу, а агент берет на себя чтение контекста проекта, изменения кода и часть проверок. Для [[ai-engineering]] это пример developer tooling, где LLM становится операционным участником workflow, а не только чат-помощником.

## Caveats

- Для реальных задач нужен настроенный доступ к выбранному LLM-провайдеру.
- Долгие и параллельные сессии лучше запускать в отдельных рабочих директориях.
- Автоматические изменения кода всё равно требуют review gates: тестов, diff review и контроля области изменений.

## Связанные страницы

- [[agentic-coding-workflows]]
- [[ai-engineering]]
- [[openai-codex-python-sdk]]
