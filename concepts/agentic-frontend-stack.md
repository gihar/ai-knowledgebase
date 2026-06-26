---
title: Agentic frontend stack
created: 2026-06-26
updated: 2026-06-26
type: concept
tags: [agent, tool-use, workflow, ai-engineering, architecture-pattern, devtools]
sources: [raw/articles/copilotkit-frontend-stack-for-ai-agents-2026-05-20.md]
confidence: medium
---

# Agentic frontend stack

Agentic frontend stack — архитектурный слой между AI-агентом и пользователем, который делает агентный backend пригодным для реального продукта: stateful, inspectable, безопасным, управляемым через UI и способным показывать действия, а не только отвечать текстом.

## Почему это важно

В agent-native продуктах сложность часто находится не только в модели или agent loop, а в пользовательском интерфейсе вокруг него. Пользователь должен видеть, что делает агент, понимать state, подтверждать рискованные действия, возвращаться к долгим runs и взаимодействовать с результатами через формы, таблицы, charts и другие UI-объекты.

Статья про [[copilotkit]] формулирует это как «слой между агентом и пользователями»: агентный продукт выигрывает не только моделью, а интерфейсом, который делает модель usable, stateful и safe.^[raw/articles/copilotkit-frontend-stack-for-ai-agents-2026-05-20.md]

## Типовые компоненты

Agentic frontend stack обычно включает:

- **Agent/UI protocol** — event stream между frontend и agent backend: текст, tool calls, state updates, status events.
- **Runtime layer** — server-side слой, который принимает frontend-запросы, запускает agents и stream events обратно.
- **Shared state** — синхронизация application state и agent state.
- **Frontend tools** — функции UI/app, которые агент может вызвать по schema.
- **Human-in-the-loop** — approvals, confirmations, edits и interrupts до выполнения действия.
- **Persistent threads** — долговременные conversations/runs между устройствами и сессиями.
- **Generative UI** — возможность агенту рендерить компоненты, формы, charts или sandboxed HTML.
- **Inspector/debugging** — просмотр raw events, context, tools, schemas и connected agents.
- **Coding-agent context bridge** — MCP/llms.txt/docs-канал, чтобы coding agents строили UI по актуальным API.

## Спектр Generative UI

В статье выделены три режима generative UI:

| Режим | Суть | Плюс | Риск |
|---|---|---|---|
| Controlled | Разработчик заранее создаёт components, агент выбирает и заполняет данные | Pixel-perfect, design-system control | Большое число components раздувает tool context и путает агента |
| Declarative / A2UI | Агент emits schema/layout из component catalog | Flat token cost при росте library | Layout принадлежит LLM, output нестабилен |
| Open-ended / MCP Apps | Агент генерирует raw HTML в sandboxed iframe | Максимальная гибкость для одноразовых UI | Не подходит для повторяемых production surfaces |

Практическое правило: чем важнее контроль, бренд, legal/compliance и предсказуемость, тем ближе нужно быть к Controlled UI; чем больше exploration и one-off interaction, тем допустимее open-ended UI.^[raw/articles/copilotkit-frontend-stack-for-ai-agents-2026-05-20.md]

## Связь с AI-инжинирингом

Agentic frontend stack — часть [[ai-engineering]], потому что превращает агентный интерфейс в поддерживаемый software artifact: его можно версионировать, тестировать, отлаживать, подключать к observability и развивать независимо от модели.

Он также связан с [[dynamic-workflows]] и [[agentic-coding-workflows]]: долгие runs, tool loops и multi-agent orchestration становятся понятнее пользователю, если события и state имеют явный UI/protocol слой.

## Открытые вопросы

- Насколько широко AG-UI/A2UI станут industry-standard, а не ecosystem-specific протоколами.
- Как балансировать autonomous actions и human-in-the-loop, чтобы не превратить агента в медленный wizard.
- Как валидировать generative UI, особенно если агент может emit schema или HTML.
- Как хранить feedback signals без нарушения privacy/compliance.

## Связанные страницы

- [[copilotkit]]
- [[ai-engineering]]
- [[agentic-coding-workflows]]
- [[dynamic-workflows]]
- [[agent-looping]]
