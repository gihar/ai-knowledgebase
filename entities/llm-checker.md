---
title: llm-checker
created: 2026-06-02
updated: 2026-06-02
type: entity
tags: [devtools, inference, gpu, quantization, cost]
sources: [raw/articles/llm-checker-local-llm-recommendations-2026-06-02.md]
confidence: medium
---

# llm-checker

`llm-checker` — CLI-утилита для оценки того, какие локальные LLM имеет смысл запускать на конкретном компьютере. Она анализирует CPU, GPU, RAM, backend ускорения и затем рекомендует модели под категории вроде coding, reasoning и multimodal. Для практики [[local-llm-hardware-fit]] это полезный предварительный фильтр перед загрузкой моделей в Ollama, LM Studio или Open WebUI.

## Ключевые команды

```bash
npm install -g llm-checker
llm-checker hw-detect
llm-checker recommend --category coding
```

По публичному README/GitHub и npm-описанию инструмент также поддерживает `check`, `installed`, `search`, `ollama-plan`, `verify-context`, `toolcheck`, `gpu-plan` и MCP-related команды. Это расширяет сценарий от простого выбора модели до планирования контекста, параллелизма и проверки совместимости с tool calling.

## Практическое значение

Главная ценность `llm-checker` — сократить цикл проб и ошибок при локальном запуске моделей. Вместо подхода «скачать модель и проверить, запустится ли» пользователь сначала получает hardware-aware shortlist и команды вроде `ollama pull ...`. Это особенно актуально для [[ai-engineering]], где локальная модель должна быть не просто установлена, а предсказуемо работать в workflow разработки, прототипирования или персонального ассистента.

## Caveats

- Рекомендации зависят от актуальности каталога моделей и эвристик оценки памяти/VRAM.
- Социальный пост и скриншот показывают один пример; перед production-использованием стоит проверять скорость, качество и лимиты контекста на своих задачах.
- Для coding-задач hardware fit не заменяет оценку качества модели на реальном коде; это только фильтр совместимости.

## Связанные страницы

- [[local-llm-hardware-fit]]
- [[ai-engineering]]
- [[agentic-coding-workflows]]
