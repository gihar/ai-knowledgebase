---
title: ant CLI
created: 2026-06-03
updated: 2026-06-03
type: entity
tags: [agent, tool-use, workflow, automation, api, devtools]
sources: [raw/articles/anthropic-ant-cli-claude-platform-2026-06-03.md]
confidence: medium
---

# ant CLI

`ant` — CLI для Claude Platform, который, согласно пересланному посту, позволяет вызывать API-ресурсы Anthropic из терминала: `messages`, `models`, `files` и другие подкоманды. Он связывает Claude API с привычными developer workflows: shell-пайпами, YAML-конфигурациями, TUI-выводом и CI.

## Основные возможности

- Интерактивная авторизация через OAuth: `ant auth login`; для headless-сред можно вывести URL через `ant auth login --no-browser`.
- Запуск Claude Platform API-эндпоинтов из терминала, включая Messages API.
- Передача запросов через типизированные флаги или YAML из пайпа.
- Подключение файлов через `@path`.
- Преобразование ответов через `--transform`.
- Форматы вывода: `json`, `yaml`, `jsonl` и `explore` с TUI, поиском и сворачиваемыми секциями.
- Управление Claude Managed Agents локально и из CI, включая `ant beta:agents update`.

## Managed Agents как Git/CI workflow

Пост описывает паттерн, где конфигурация Claude Managed Agent хранится в Git как YAML, а CI синхронизирует её с Claude Platform. Это превращает агента в версионируемый артефакт инфраструктуры: изменения можно ревьюить, применять из pipeline и воспроизводить между окружениями.

## Связь с кодовыми агентами

`ant` может быть backend-инструментом для [[agentic-coding-workflows]]: кодовый агент вроде Claude Code вызывает CLI, читает результаты и не требует отдельного glue-кода. Упомянутый навык `/claude-api` делает API-операции доступными из агентного интерфейса, аналогично тому, как [[opencode]] и [[openai-codex-python-sdk]] расширяют способы автоматизации разработки.

## Открытые вопросы

- Нужно проверить фактические команды установки и текущую доступность CLI через официальные источники Anthropic.
- `beta:agents` указывает на beta-статус Managed Agents API; команды и формат YAML могут измениться.
- OAuth-токены, сохранённые локально, требуют понятной политики хранения и ротации на рабочих станциях и CI.

## Связанные страницы

- [[agentic-coding-workflows]]
- [[ai-engineering]]
- [[opencode]]
- [[openai-codex-python-sdk]]
