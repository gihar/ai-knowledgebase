---
title: CopilotKit
created: 2026-06-26
updated: 2026-06-26
type: entity
tags: [agent, tool-use, workflow, ai-engineering, devtools, platform, open-source]
sources: [raw/articles/copilotkit-frontend-stack-for-ai-agents-2026-05-20.md]
confidence: medium
---

# CopilotKit

CopilotKit — open-source frontend stack для AI-агентов: набор React/Frontend SDK, runtime, hooks и UI-компонентов, который соединяет пользовательский интерфейс с агентным backend через [[agentic-frontend-stack]] и протокол AG-UI.

## Ключевая идея

CopilotKit исходит из тезиса, что agent-native продукту недостаточно backend-агента. Нужен отдельный interface layer между агентом и пользователем: chat components, shared state, tool calling, human-in-the-loop approvals, persistent threads, generative UI, headless UI и debugging/inspection.

В статье CopilotKit описывается как слой между агентом и пользователями: модель решает задачу, но именно интерфейс делает её usable, stateful и safe для реальных людей.^[raw/articles/copilotkit-frontend-stack-for-ai-agents-2026-05-20.md]

## Архитектура

CopilotKit делит систему на три слоя:

1. **Frontend / app** — hooks и components для регистрации frontend-tools, передачи context и rendering agent UI.
2. **Runtime / server** — принимает frontend-запросы, запускает agents и стримит events обратно.
3. **Agent / any framework** — любой backend, который говорит на AG-UI; в статье упомянуты Built-in Agent, LangGraph, Mastra, Pydantic AI, CrewAI, Google ADK, Microsoft Agent Framework, AWS Strands и другие.

Такой слой позволяет заменить agent backend без переписывания UI: `<CopilotChat />`, hooks и components остаются теми же, пока backend говорит на AG-UI.^[raw/articles/copilotkit-frontend-stack-for-ai-agents-2026-05-20.md]

## Возможности

- **Chat components**: `CopilotChat`, `CopilotSidebar`, `CopilotPopup`, `CopilotChatView`.
- **Context/readables**: приложение может показывать агенту current user, selected items, loaded data и другой state.
- **Frontend tools**: функции frontend можно регистрировать как tools, которые агент вызывает через описание и schema.
- **Persistent threads**: conversation, state и tool calls сохраняются между сессиями и устройствами.
- **Generative UI**: агент рендерит компоненты, charts, forms или sandboxed HTML вместо текстового описания.
- **Headless UI**: primitives для полностью кастомных agent interfaces.
- **CopilotKit Inspector**: отладка raw AG-UI event stream, connected agents, tools, schemas и context.
- **MCP server**: `https://mcp.copilotkit.ai/mcp` для coding agents вроде Claude Code, Codex и Cursor, чтобы они получали актуальные API signatures и examples.

## Практическое значение

Для AI-продуктов CopilotKit закрывает проблему «последней мили»: как показать пользователю действия агента, синхронизировать state, дать approve/feedback и отладить происходящее. Это связывает CopilotKit с [[ai-engineering]], потому что агентный интерфейс становится поддерживаемым engineering artifact, а не разовым chat prompt.

## Caveats

- Утверждения про adoption, Fortune 500 и 30k+ GitHub stars взяты из статьи CopilotKit и требуют отдельной проверки при использовании в внешней аналитике.
- Подход сильно ориентирован на frontend/React ecosystem, хотя статья утверждает поддержку разных frameworks и server adapters.
- Для Generative UI есть trade-off: Controlled UI даёт контроль, но растит tool context; declarative A2UI снижает token cost, но отдаёт layout LLM; open-ended HTML гибок, но подходит скорее для одноразовых интерфейсов.

## Связанные страницы

- [[agentic-frontend-stack]]
- [[ai-engineering]]
- [[agentic-coding-workflows]]
- [[dynamic-workflows]]
