---
title: OpenCode
created: 2026-06-03
updated: 2026-06-05
type: entity
tags: [agent, devtools, open-source, ai-engineering, automation]
sources: [raw/articles/opencode-ai-coding-agent-2026-06-03.md, raw/articles/opencode-rules-agents-config-2026-06-05.md]
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

## Конфигурация правил и агентов

Для настройки поведения [[opencode]] источник фиксирует несколько уровней правил:

- проектные инструкции в `AGENTS.md` в корне репозитория; TUI-команда `/init` может сгенерировать или обновить этот файл после анализа проекта;
- глобальные инструкции для всех проектов в `~/.config/opencode/AGENTS.md`;
- дополнительные instruction-файлы через `instructions` в `opencode.json`, например `CONTRIBUTING.md`, `docs/guidelines.md` или `.cursor/rules/*.md`;
- отдельные агенты в `~/.config/opencode/agents/*.md`, где frontmatter задает описание, режим, температуру и permissions, а тело файла выступает как инструкция агента;
- prompt-файлы для конкретных агентов через `opencode.json`, например `"prompt": "{file:./prompts/code-review.txt}"`.

Практический вывод: для обычной настройки поведения OpenCode лучше начинать с `AGENTS.md`, для постоянных личных предпочтений — с глобального `~/.config/opencode/AGENTS.md`, а для специализированных режимов вроде strict code review — с отдельного agent-файла. Это связывает OpenCode с [[agentic-coding-workflows]] как с инструментом, где правила проекта и permissions становятся частью операционного контура агента.

## Приоритет инструкций и fallback

Если в проекте есть и `AGENTS.md`, и `CLAUDE.md`, OpenCode должен брать `AGENTS.md`. `CLAUDE.md` используется как fallback: локально — если нет проектного `AGENTS.md`, глобально — через `~/.claude/CLAUDE.md`, если нет `~/.config/opencode/AGENTS.md`. Для OpenCode предпочтительны нативные файлы `AGENTS.md`, `~/.config/opencode/AGENTS.md`, `opencode.json` и `~/.config/opencode/agents/*.md`.

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
