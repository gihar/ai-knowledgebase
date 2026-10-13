---
title: Turn Inspector — визуализация контекстного окна Claude Code
created: 2026-10-13
updated: 2026-10-13
type: entity
tags: [agent, devtools, observability, workflow, open-source, tool-use]
sources: [raw/articles/turn-inspector-forwarded-2026-10-13.md]
confidence: medium
---

# Turn Inspector

[Turn Inspector](https://www.aitmpl.com/component/mods/ui/turn-inspector) — мод из [Claude Code Templates](https://github.com/davila7/claude-code-templates), показывающий в боковой панели, как по запросам модели меняется заполнение контекстного окна. В [пересланном посте](../raw/articles/turn-inspector-forwarded-2026-10-13.md) приложена видеодемонстрация интерфейса. Это инструмент наблюдения за [[claude-code]], а не мод для изменения промпта или автоматической экономии токенов.

## Что видно

- Общий размер входа/выхода и процент заполнения окна; ходы сгруппированы по исходному запросу пользователя.
- Разворачиваемые категории входа: система, инструменты и память; ранние ходы; новое сообщение или результат инструмента.
- Категории выхода: thinking, текстовый ответ, вызовы инструментов; при сокращении входа отмечается compaction.
- Видео показывает рост окна в последовательности ходов и отдельные блоки `System, tools & memory`, `Earlier turns`, `User message`, `Tool result`, `Thinking`, `Tool use`, `Text response`.

**Точность:** по [описанию автора](https://www.aitmpl.com/component/mods/ui/turn-inspector) общий input/output берётся из API usage конкретного запроса, но величины **отдельных блоков с `~` — оценки**, распределённые по размеру текста. Это схема состава и оценки токенов, **не полный дамп буквального системного промпта, содержимого памяти или скрытого reasoning**. Для возобновлённой сессии оценка системной части также может быть приблизительной.

## Использование и ограничения

```bash
npx claude-code-templates@latest --mod ui/turn-inspector
```

Согласно странице мода, он устанавливается в `.claude/skills/turn-inspector/`; открыть панель — `/turns`, очистить историю — `/turns clear`, закрыть — `/turns stop`. Mods включены по умолчанию в Claude Code 2.1.287+; в версиях 2.1.259–2.1.286 нужен `CLAUDE_CODE_ENABLE_FUNCTION_HOOKS=1`. Записываются события с момента загрузки мода; запросы субагентов не отображаются (для них упомянут отдельный `agent-flow`).

Не установлен и не испытан здесь. Перед запуском `npx ...@latest` следует проверить версию пакета, права мода и сетевое поведение. Видимость токенов помогает анализировать накладные расходы [[agent-skills]] и длинных [[dynamic-workflows]], но сами цифры не доказывают, что какую-либо часть контекста можно удалить без потери качества.

## Связанные страницы

- [[claude-code]]
- [[agent-skills]]
- [[dynamic-workflows]]
