---
source_url: telegram-forwarded-post
ingested: 2026-06-05
sha256: eef73e2eae817a5d03c244ce7ae9ee381f2d0a154bdaf492a7c10be7dfca631c
---
# OpenCode rules / agents config

Источник: сообщение пользователя в Telegram от 2026-06-05.

```text
Да, Лёша, поправляюсь: для OpenCode, не OpenClaude.

В OpenCode “системный промпт” обычно меняется не через --system-prompt-file, а через rules / agents config.

1. Для проекта: AGENTS.md

В корне репозитория создай:

touch AGENTS.md


И напиши туда правила:

# Инструкции для OpenCode

- Отвечай на русском.
- Перед изменениями сначала кратко формулируй план.
- После правок запускай релевантные тесты.
- Не меняй публичные API без явного запроса.
- Для frontend используй существующие компоненты и дизайн-систему.


OpenCode будет подхватывать AGENTS.md при запуске в этом проекте.

Можно создать/обновить автоматически через TUI-команду:

/init


Она просканирует репозиторий и сделает проектные инструкции.

2. Глобальные правила для всех проектов

Файл:

~/.config/opencode/AGENTS.md


Создать:

mkdir -p ~/.config/opencode
nano ~/.config/opencode/AGENTS.md


Пример:

# My OpenCode preferences

- Отвечай кратко.
- Всегда объясняй рискованные изменения.
- Не запускай destructive-команды без подтверждения.
- Предпочитай минимальные изменения вместо больших переписываний.


Это будет применяться ко всем сессиям OpenCode.

3. Подключить дополнительные instruction-файлы через opencode.json

Можно не складывать всё в AGENTS.md, а подключить отдельные файлы:

{
  "$schema": "https://opencode.ai/config.json",
  "instructions": [
    "CONTRIBUTING.md",
    "docs/guidelines.md",
    ".cursor/rules/*.md"
  ]
}


Файл можно положить:

- в проект: opencode.json
- глобально: ~/.config/opencode/opencode.json

Все эти инструкции будут объединены с AGENTS.md.

4. Если нужен именно отдельный agent с кастомным system prompt

Для OpenCode можно описать отдельного агента.

Глобально:

mkdir -p ~/.config/opencode/agents
nano ~/.config/opencode/agents/review.md


Пример:

---
description: Reviews code for quality, security and maintainability
mode: subagent
temperature: 0.1
permission:
  edit: deny
  bash: deny
---

You are in strict code review mode.

Focus on:
- bugs
- security risks
- test gaps
- maintainability
- architectural regressions

Do not edit files. Return only findings and recommendations.


Имя файла становится именем агента: review.

5. Через opencode.json можно задать prompt-файл агенту

Например:

{
  "$schema": "https://opencode.ai/config.json",
  "agent": {
    "review": {
      "prompt": "{file:./prompts/code-review.txt}"
    }
  }
}


Тогда ./prompts/code-review.txt будет системным промптом конкретного агента.

6. Fallback от Claude Code

OpenCode умеет читать Claude Code-файлы как fallback:

- проектный CLAUDE.md — если нет AGENTS.md;
- глобальный ~/.claude/CLAUDE.md — если нет ~/.config/opencode/AGENTS.md.

Но для OpenCode правильнее использовать именно:

AGENTS.md
~/.config/opencode/AGENTS.md
opencode.json
~/.config/opencode/agents/*.md


Приоритет

OpenCode ищет правила примерно так:

1. Локальные проектные файлы: AGENTS.md, затем CLAUDE.md
2. Глобальный файл: ~/.config/opencode/AGENTS.md
3. Claude fallback: ~/.claude/CLAUDE.md

Если есть и AGENTS.md, и CLAUDE.md, OpenCode берёт AGENTS.md.

Короткий ответ

Для обычной настройки поведения OpenCode:

nano AGENTS.md


Для глобальной настройки:

nano ~/.config/opencode/AGENTS.md


Для отдельного кастомного агента:

nano ~/.config/opencode/agents/my-agent.md


А если нужен полноценный prompt-файл для агента — укажи его в opencode.json через:

"prompt": "{file:./prompts/my-agent.txt}"
```
