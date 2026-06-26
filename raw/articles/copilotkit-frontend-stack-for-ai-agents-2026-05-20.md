---
source_url: https://www.copilotkit.ai/blog/frontend-stack-for-ai-agents
ingested: 2026-06-26
sha256: d4d0313a5eafdd3155d0797dcffef64cf0d4dbca62bb02d594524152239b03e1
---

# CopilotKit — полный фронтенд-стек для AI-агентов

**Источник:** CopilotKit Blog  
**Авторы:** Anmol Baranwal и Nathan Tarbert  
**Дата:** 20 мая 2026

## Главный тезис

Каждая крупная категория ПО перестраивается вокруг агентов. Вопрос уже не в том, будет ли у продукта AI-агент, а в том, достаточно ли хорош интерфейс вокруг него для реальных пользователей.

**CopilotKit** позиционируется как open-source фронтенд-стек для AI-агентов. Он используется в production у большинства компаний Fortune 500, а команда CopilotKit стоит за **AG-UI** — открытым протоколом взаимодействия агент–пользователь, который, по статье, уже принят Google, AWS, Microsoft, LangChain, Mastra и другими. Идея CopilotKit: весь UI постепенно становится AI.

CopilotKit даёт разработчику набор инструментов для сборки, отладки и поставки интерфейсного слоя между агентом и пользователем: chat-компоненты, hooks, persistent memory, generative UI, headless UI для кастомных интерфейсов, Inspector для отладки и MCP-сервер для coding agents.

CopilotKit open-source и имеет 30k+ звёзд на GitHub.

## Что покрывает статья

В статье разбираются:

- CopilotKit как набор building blocks для Agent UI;
- подключение агента к приложению за 5 минут;
- варианты подключения агента к frontend и когда какой выбирать;
- прямое подключение LLM;
- agent frameworks и 13+ интеграций;
- собственный backend с кастомной логикой;
- persistent memory между сессиями и устройствами;
- отладка через CopilotKit Inspector;
- MCP-сервер CopilotKit для coding agents;
- Generative UI: агенты, которые «поставляют» собственные интерфейсы;
- Headless UI для полностью кастомных интерфейсов;
- VSCode Extension для preview, inspection и итераций над Agent UI;
- self-improving agents с continuous learning.

## 1. CopilotKit: building blocks для поставки Agent UI

Если каждая новая способность агента требует отдельного frontend-спринта, агент не является по-настоящему автономным. Это всего лишь backend API с очень дорогим chat-интерфейсом.

CopilotKit отделяет агента от interface layer. Generative UI позволяет агенту рендерить собственные компоненты. Shared state держит агента и UI синхронизированными. Human-in-the-loop даёт пользователю возможность approve до выполнения действия. Всё это соединено через **AG-UI**, поэтому backend агента можно заменить, а frontend останется тем же.

Архитектура состоит из трёх слоёв:

### Слой 1: Frontend — ваше приложение

Hooks и компоненты позволяют подключить приложение: регистрировать tools, которые может вызывать агент, передавать агенту context и получать agent instances.

### Слой 2: Runtime — ваш server

Runtime принимает запросы от frontend, запускает агентов и стримит события обратно. Это несколько строк настройки; runtime обслуживает всё между моделью и пользователем.

### Слой 3: Agent — любой framework

Подходит всё, что говорит на **AG-UI** — event-протоколе между агентами и UI. События могут означать: «стримится текст», «агент хочет вызвать tool», «state изменился». Есть 13+ готовых интеграций, но можно собрать свою.

Из коробки также доступны:

- **Persistent threads** — conversations, state и tool calls синхронизируются между устройствами и сессиями.
- **Generative UI** — агент вместо текстового ответа рендерит реальные компоненты: chart, booking form и т.п.
- **MCP server for coding agents** — coding agent получает актуальные docs и snippets без stale training data.
- **Agent Inspector** — browser-panel для отладки actions, readables, agent status, messages и context.
- **VSCode extension** — тот же inspector внутри редактора и live preview agent-rendered components без запуска полного приложения.

## 2. Как добавить агента в приложение за 5 минут

Самый быстрый путь — CLI.

Создать новое full-stack приложение:

```bash
npx copilotkit@latest create
```

Добавить CopilotKit в существующий проект и выбрать agent framework:

```bash
npx copilotkit@latest init
```

Команды устанавливают packages, настраивают provider, создают runtime endpoint и добавляют chat component.

### `useAgentContext`

`useAgentContext` делает state приложения видимым для агента. Всё, что передано в context — current user, selected items, loaded data — становится частью контекста LLM. Агент знает то, что знает ваше приложение.

### `useFrontendTool`

`useFrontendTool` раскрывает любую функцию приложения как tool, который агент может вызвать. Разработчик описывает, что делает tool, а агент решает, когда использовать его. Модель не мутирует state напрямую.

Пример из статьи:

```tsx
// ... useAgentContext

useFrontendTool({
  name: "addExpense",
  description: "Add a new expense when the user mentions spending money on something.",
  parameters: z.object({
    description: z.string().describe("What the expense was for, e.g. Lunch, Taxi, Coffee"),
    amount: z.number().describe("How much was spent in dollars"),
    category: z.string().describe("Food, Transport, Entertainment, Health, or Other"),
  }),
  handler: async ({ description, amount, category }) => {
    setExpenses((prev) => [
      ...prev,
      { id: Date.now(), description, amount, category },
    ]);
    return `Added $${amount} for ${description}`;
  },
  // optional: render the component in chat while/after the tool runs
  render: ({ status, args }) => (
    <ExpenseCard
      status={status}
      description={args.description}
      amount={args.amount}
      category={args.category}
    />
  ),
});
```

### `useAgent`

`useAgent` даёт live connection к агенту: messages, current state и running status. Его можно читать или обновлять напрямую из UI.

```tsx
// Programmatically access and control your agents
const { agent } = useAgent({ agentId: "my_agent" });

// Render and update your agent's state
return (
  <div>
    <h1>{agent.state.city}</h1>
    <button onClick={() => agent.setState({ city: "NYC" })}>
      Set City
    </button>
  </div>
);
```

Базовый набор дополняют built-in chat components (`CopilotChat`, `CopilotSidebar`, `CopilotPopup`, `CopilotChatView`) и hooks под конкретные задачи: `useHumanInTheLoop` для approval flows, `useComponent` для generative UI, `useThreads` для persistence.

### File and image attachments

Пользователи не только печатают. CopilotKit позволяет отправлять images, audio, video и documents агенту вместе с сообщениями. Включается одним prop:

```tsx
import { CopilotChat } from "@copilotkit/react-core/v2";

<CopilotChat
  agentId="my-agent"
  attachments={{ enabled: true }}
/>
```

Пользователи могут нажать attachment button или перетащить файлы. Это работает с Built-in Agent, поддерживаемыми frameworks или собственным backend. Не все модели поддерживают все file types, поэтому для unsupported cases нужен `onError` callback.

## 3. Подключение агента к frontend: когда какой путь выбирать

После настройки приложения нужно выбрать, что работает за runtime. Не всегда нужен полноценный agent framework — всё зависит от задачи и того, что уже есть.

Ключевой момент: каждый агент говорит на **AG-UI**, открытом bidirectional protocol для agent-user interaction. Поэтому frontend не меняется независимо от backend. Можно заменить Built-in Agent на LangGraph, а `<CopilotChat />`, hooks и components останутся теми же.

### Path 1: подключить любую LLM напрямую

Если нужен агент, который aware of app и может выполнять действия, достаточно `BuiltInAgent`. Runtime берёт на себя model call, tool loop и streaming. Всё живёт в одном endpoint, например `app/api/copilotkit/route.ts`.

```ts
import {
  CopilotRuntime,
  copilotRuntimeNextJSAppRouterEndpoint,
} from "@copilotkit/runtime";
import { BuiltInAgent } from "@copilotkit/runtime/v2";
import { NextRequest } from "next/server";

const runtime = new CopilotRuntime({
  agents: new BuiltInAgent({ model: "openai/gpt-5.5" }),
});

export const POST = async (req: NextRequest) => {
  const { handleRequest } = copilotRuntimeNextJSAppRouterEndpoint({
    runtime,
    endpoint: "/api/copilotkit",
  });
  return handleRequest(req);
};
```

Чтобы переключиться на другого LLM provider, достаточно заменить model string в `BuiltInAgent` и добавить соответствующий key в `.env.local`.

```ts
// Anthropic
const builtInAgent = new BuiltInAgent({
  model: "anthropic:claude-opus-4-6",
});

// Google
const builtInAgent = new BuiltInAgent({
  model: "google/gemini-2.5-pro",
});
```

Reasoning models вроде `openai:o3` и `openai:o4-mini` тоже поддерживаются: можно передавать `reasoningEffort`. Для Anthropic extended thinking используется `budgetTokens`; reasoning stream рендерится прямо в chat UI.

```ts
// Anthropic with extended thinking
const agent = new BuiltInAgent({
  model: "anthropic:claude-sonnet-4-6",
  providerOptions: {
    anthropic: { thinking: { type: "enabled", budgetTokens: 10000 } },
  },
});
```

Этот путь хорош для solo developers, in-app assistants, chatbots и prototypes. Поверх него можно использовать MCP Apps middleware, чтобы возвращать интерактивные MCP Apps — forms, canvases, pickers — прямо в chat.

```ts
const agent = new BuiltInAgent({
  model: "openai/gpt-5.5",
  prompt: "You are a helpful assistant.",
}).use(
  // describe a diagram in chat, Excalidraw MCP server returns an interactive UI
  new MCPAppsMiddleware({
    mcpServers: [
      { type: "http", url: "https://mcp.excalidraw.com/mcp", serverId: "excalidraw" },
    ],
  }),
);
```

### Path 2: agent frameworks

CopilotKit поставляет first-party integrations для 13+ agent frameworks через **AG-UI**. Если агент уже работает в каком-то framework, можно просто направить runtime на endpoint агента через `HttpAgent`.

```ts
import {
  CopilotRuntime,
  ExperimentalEmptyAdapter,
  copilotRuntimeNextJSAppRouterEndpoint,
} from "@copilotkit/runtime";
import { HttpAgent } from "@ag-ui/client";
import { NextRequest } from "next/server";

const serviceAdapter = new ExperimentalEmptyAdapter();
const runtime = new CopilotRuntime({
  agents: {
    my_agent: new HttpAgent({ url: "http://localhost:8000/" }),
  }
});

export const POST = async (req: NextRequest) => {
  const { handleRequest } = copilotRuntimeNextJSAppRouterEndpoint({
    runtime,
    serviceAdapter,
    endpoint: "/api/copilotkit",
  });
  return handleRequest(req);
};
```

Паттерн одинаковый: агент emits events через AG-UI, CopilotKit runtime говорит AG-UI на другой стороне, а tools, shared state и approval flows автоматически появляются в UI. Дополнительный glue code не нужен.

Поддерживаются LangGraph, TanStack, Mastra, Pydantic AI, CrewAI, Microsoft Agent Framework, Google ADK, AWS Strands, LlamaIndex, Agno, AG2, Deep Agents, Open Agent Spec (`agent-spec`), A2A и другие. Этот путь хорош для команд со сложными workflows, multi-agent orchestration или уже существующим агентом.

### Path 3: собственный backend — custom logic, any server

Если есть собственная AI-инфраструктура — internal LLM proxy, fine-tuned model endpoint или custom tool dispatch — можно запускать `CopilotRuntime` на своём server. CopilotKit берёт на себя protocol layer между backend и frontend без обязательного agent framework.

```ts
import express from "express";
import { CopilotRuntime, BuiltInAgent } from "@copilotkit/runtime/v2";
import { createCopilotExpressHandler } from "@copilotkit/runtime/v2/express";

const runtime = new CopilotRuntime({
  agents: {
    default: new BuiltInAgent({ model: "openai/gpt-5" }),
  },
});

const app = express();

// Mount the CopilotKit router — creates Express routes under /api/copilotkit
app.use(
  createCopilotExpressHandler({
    runtime,
    basePath: "/api/copilotkit",
    cors: true,
  }),
);
```

После запуска runtime frontend указывает на него:

```tsx
<CopilotKit runtimeUrl="http://localhost:4000/api/copilotkit">
  <YourApp />
</CopilotKit>
```

Подход работает с Next.js, Express, Hono, Bun, Deno, Cloudflare Workers, React Router, TanStack Start, Elysia и другими. Он подходит командам с existing AI services, custom infrastructure или строгими deployment requirements.

## 4. Persistent memory между сессиями и устройствами

Большинство агентов каждый раз стартуют с нуля: пользователь закрывает вкладку, возвращается завтра, и агент не знает, над чем он работал. Для demo это терпимо, но для production — серьёзный блокер.

Без threads каждая agent session заканчивается вместе с вкладкой. С threads run становится частью state приложения. Один hook даёт ChatGPT-like thread sidebar с persistent memory:

```ts
const {
  threads,
  renameThread,
  archiveThread,
  deleteThread,
  hasMoreThreads,
  fetchMoreThreads,
} = useThreads();
```

Threads в CopilotKit работают иначе: runs живут на server и стримятся через AG-UI, поэтому пользователь может уйти от агента в любой момент. Вернувшись позже на другом устройстве, он увидит run ровно в том состоянии, где агент находится сейчас, даже если агент всё ещё прогрессирует. Thread хранит всё, что происходит между user, agent и app.

## 5. Отладка агентов через CopilotKit Inspector

Агенты часто выглядят как black box: код написан, запуск выполнен, но при странном ответе нет stack trace, только недовольный пользователь. **CopilotKit Inspector** — встроенный debugging tool поверх приложения, который показывает, что происходит между frontend и agents в real time:

- raw AG-UI event stream;
- какие agents подключены и доступны;
- agent state по мере обновления;
- frontend tools и parameter schemas;
- полный context, переданный агенту, включая readables и document context.

В development Inspector включён по умолчанию. Отключение:

```tsx
<CopilotKit showDevConsole={false}>
  {children}
</CopilotKit>
```

## 6. CopilotKit MCP Server для coding agents — Claude Code, Codex, Cursor

Если разработка идёт с coding agent вроде Claude Code, Cursor или Windsurf, перед написанием CopilotKit-кода полезно подключить MCP-сервер.

Coding agents часто опираются на training data, которая может быть устаревшей: deprecated hooks, старые tutorials, сломанные patterns. CopilotKit поставляет knowledge MCP server по адресу:

```text
mcp.copilotkit.ai/mcp
```

Для Claude Code команда:

```bash
claude mcp add --transport http copilotkit-mcp https://mcp.copilotkit.ai/mcp
```

Так coding agent получает live access к правильным API signatures, актуальным code examples и implementation patterns. Если tool не поддерживает MCP, можно напрямую добавить в model context:

```text
https://mcp.copilotkit.ai/llms.txt
```

## 7. Generative UI: агенты, которые поставляют собственные интерфейсы

Знакомая проблема: просишь AI сравнить три варианта — получаешь стену текста вместо таблицы. Просишь календарь — получаешь prose description. Проблема не в модели: она умеет отрендерить таблицу, но не знает, что ей разрешено это сделать.

**Generative UI** — слой, который позволяет агентам перестать описывать и начать показывать.

В статье выделяются три паттерна; спектр идёт от большего контроля к большей гибкости. CopilotKit поддерживает все три.

### Controlled

Разработчик заранее строит components, агент выбирает, какой показать, и заполняет его данными. Например, пользователь просит spending breakdown, агент вызывает `pieChart` и стримит данные в него. Дизайн остаётся pixel-perfect и соответствует design system. Hook — `useComponent`.

Ограничение: каждый registered component — это tool definition в context агента. После примерно 25 components агент начинает путаться: pie chart и donut chart оба «show proportions», и он может выбрать не то.

### Declarative — A2UI

Вместо pre-built component для каждого случая агенту дают schema, и он сам собирает layout. Один tool, много UI, flat token cost по мере роста library. Добавили новый card type — агент сразу может его использовать. Подход построен на Google A2UI protocol.

Ограничение: layout принадлежит LLM, поэтому output может отличаться от запуска к запуску. Это не подходит для legal disclosures, marketing surfaces и любых мест, где важно точное pixel placement.

### Open-ended — MCP Apps / Open Generative UI

Агент пишет raw HTML, приложение рендерит его в sandboxed iframe. Нет catalog, schema и правил. Это хорошо для одноразовых интерфейсов: «покажи, как работают электроны», «сделай странный bar chart моих последних 10 queries». Но не для интерфейса, который реальный пользователь увидит дважды.

Пример: «Build a neo-brutalism themed calculator» — агент на месте генерирует полный interactive HTML.

## 8. Headless UI: полностью кастомные agent interfaces

Prebuilt components (`CopilotChat`, `CopilotSidebar`, `CopilotPopup`) закрывают большинство случаев, но не каждому продукту нужна floating chat bubble. Агент может жить внутри dashboard, отвечать через voice interface или показывать progress в sidebar, который выглядит как часть продукта.

Если нужно только слегка изменить layout или style prebuilt components, проще использовать slot system. **Headless UI** нужен для более глубоких изменений: полностью другой layout, non-chat interface или embedding глубоко в существующий UI.

Две основные primitives:

- `useAgent` — даёт messages, state и run status;
- `useCopilotKit` — даёт `copilotkit.runAgent()` для запуска агента из любого места.

```tsx
import { useAgent, useCopilotKit } from "@copilotkit/react-core/v2";

export default function Chat() {
  const { agent } = useAgent();
  const { copilotkit } = useCopilotKit();

  return (
    <div>
      {agent.messages.map(m => (
        <p key={m.id}>{m.content}</p>
      ))}
      <button onClick={() => copilotkit.runAgent({ agent })}>
        {agent.isRunning ? "Thinking..." : "Send"}
      </button>
    </div>
  );
}
```

## 9. VSCode Extension: preview, inspect, iterate over Agent UI

CopilotKit VSCode extension приносит в editor четыре инструмента, чтобы итерироваться без запуска полного приложения:

- **Hook Explorer (Generative UI)** — сканирует workspace на CopilotKit hooks, рендерит generative UI с auto-generated form controls. Работает offline, без agent run.
- **A2UI Catalog Preview** — live preview catalog components; при сохранении preview hot-reloads.
- **Playground** — полноценная chat surface, которая реально запускает агента внутри editor, detects hooks, wires them to local runtime и hot-reloads on save.
- **AG-UI Inspector** — realtime stream всех AG-UI events, которые emit runtime, с color coding и filters.

Установка из терминала:

```bash
code --install-extension copilotkit.copilotkit
```

## 10. Self-improving agents с continuous learning

Сейчас агенты часто остаются ровно настолько умными, насколько были в день релиза. Если агент каждый раз ошибается при export CSV, он будет ошибаться, пока команда не заметит, не воспроизведёт проблему, не исправит prompt и не redeploy.

Каждое взаимодействие user-agent проходит через AG-UI как typed events. Accepted answers, edited responses, re-run tools, ignored suggestions — всё это можно capture. Thread layer делает данные persistent. Получается labeled feedback stream прямо в продукте.

Это часть **CopilotKit Intelligence Platform**:

- **Analytics & Insights** — показывает, как агент работает в production: какие flows успешны, где users drop off, что игнорируется. Данные можно SQL-query, подключать к DataDog, New Relic или другим observability tools.
- **Continuous Learning from Human Feedback (CLHF)** — сигналы из реального использования возвращаются в агента. Prompts adapt at runtime per user и per context на основе свежих outcomes. Агент улучшается по мере использования.

Статья сравнивает это с тем, как Cursor строил Composer model: каждое developer interaction было implicit training data. CopilotKit пытается принести такой loop в приложения поверх AG-UI. На момент статьи оба направления находятся в active development / early access.

## Вывод

CopilotKit — слой между агентом и пользователями.

Сложная часть agent products — не сама модель, а interface, который делает её usable, stateful и safe для реальных людей. Статья позиционирует CopilotKit как набор building blocks для SaaS copilots, productivity tools, customer support agents, internal dashboards и generative UI experiences.

Главный практический вывод: agent-native продукт требует не только backend-агента, но и отдельного interface/protocol слоя: AG-UI, shared state, human-in-the-loop, persistent threads, inspector/debugging и generative/headless UI.
