---
title: OpenAI Codex Python SDK
created: 2026-06-02
updated: 2026-06-02
type: entity
tags: [agent, tool-use, automation, api, devtools, ai-engineering]
sources: [raw/articles/openai-codex-python-sdk-2026-06-02.md]
confidence: low
---

# OpenAI Codex Python SDK

Пересланный источник утверждает, что OpenAI выпустила Python SDK для Codex, устанавливаемый как `openai-codex`, который позволяет встраивать Codex прямо в Python-приложения. Так как это быстро меняющееся утверждение из пересланного поста, а не официальная страница источника, текущая уверенность — `low` до проверки по документации OpenAI или репозиторию пакета.

## Возможности, упомянутые в источнике

Пост утверждает, что SDK умеет:

- запускать новые сессии Codex;
- выполнять отдельные шаги агента;
- передавать потоковые обновления о ходе выполнения;
- возобновлять ранее созданные сессии;
- передавать изображения в сессии;
- управлять доступом к sandbox-окружению;
- использовать уже настроенную авторизацию Codex.

## Пример паттерна

На скриншоте показаны context manager `Codex` и sandbox с правом записи в рабочую область:

```python
from openai_codex import Codex, Sandbox

with Codex() as codex:
    thread = codex.thread_start(sandbox=Sandbox.workspace_write)
    result = thread.run("Find the failing tests, explain the root cause, and propose a fix.")
    print(result.final_response)
```

Это указывает на рабочий процесс, где [[agentic-coding-workflows]] можно встраивать как Python-функции или сервисы, а не запускать через CLI-обертки.

## Почему это важно

Если релиз подтвердится, SDK упростит встраивание Codex во внутренние инструменты разработчиков, CI-ассистентов, локальную автоматизацию, review-ботов и другие системы [[ai-engineering]]. Важный сдвиг: от «вызывать агента для разработки как внешний инструмент» к «оркестрировать агента для разработки как компонент приложения».

## Изображение из источника

Пересланный пост включал скриншот минимального примера SDK: `raw/assets/openai-codex-python-sdk-example-2026-06-02.jpg`.

## Открытые вопросы

- Какая официальная документация, репозиторий пакета и changelog подтверждают релиз?
- Какие sandbox-права доступны помимо `Sandbox.workspace_write`?
- Как потоковые события представлены в API?
- Как SDK аутентифицируется и возобновляет сессии между процессами?

## Связанные страницы

- [[agentic-coding-workflows]]
- [[ai-engineering]]
