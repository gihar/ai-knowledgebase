---
source_url: https://code.claude.com/docs/en/workflows
ingested: 2026-06-09
sha256: 9efd45e69e1cc7fb793bd11bacf7557c9c85b931505fc147b32a1cb28473b97b
---
# Claude Code Dynamic Workflows: дополнительные сведения из официальной документации

Источник: ответ в Telegram от 2026-06-09 по результатам проверки официальной документации Claude Code.

```text
Нашла официальную страницу Claude Code Docs: https://code.claude.com/docs/en/workflows

Ключевое, что добавилось к посту:

## Что это официально

Dynamic Workflow — это JavaScript-скрипт, который оркестрирует subagents в фоне. Скрипт пишет Claude под конкретную задачу, а runtime исполняет его отдельно от текущего диалога.

Главная формулировка из доки: workflow нужен, когда задаче требуется больше агентов, чем один conversation может нормально скоординировать, или когда хочется, чтобы orchestration была кодом, который можно прочитать и перезапустить.

## Требования и доступность

- Нужно Claude Code v2.1.154+
- Доступно:
  - на paid plans
  - через Anthropic API access
  - Amazon Bedrock
  - Google Cloud Vertex AI
  - Microsoft Foundry
- На Pro нужно включить в `/config` в строке Dynamic workflows

## Когда использовать

Официальные примеры:
- codebase-wide bug sweep
- миграция на 500 файлов
- исследовательский вопрос с cross-check источников
- сложный план, который нужно подготовить с нескольких независимых углов

То есть это не замена обычному agent call, а режим для задач, где важны:
- много параллельных агентов
- повторяемая оркестрация
- structured aggregation
- cross-check
- контроль токенов контекста

## Сравнение с subagents / skills / agent teams

Subagents:
- Claude сам решает следующий шаг turn-by-turn
- промежуточные результаты попадают в context window
- масштаб: несколько delegated tasks за turn

Skills:
- это инструкции, которым Claude следует
- улучшают повторяемость поведения
- но orchestration всё равно остаётся внутри Claude/prompt

Agent teams:
- lead agent управляет peer sessions
- промежуточное состояние — shared task list
- масштаб: несколько долгоживущих peers

Workflows:
- следующий шаг выбирает скрипт
- промежуточные результаты живут в script variables
- повторяема именно orchestration
- масштаб: десятки/сотни agents per run

## `/deep-research`

В Claude Code уже есть bundled workflow: `/deep-research <question>`.

Он:
- запускает web searches по нескольким углам
- fetch/cross-check источников
- голосует по claim’ам
- фильтрует claim’ы, которые не прошли cross-check
- возвращает cited report

Требует доступный WebSearch tool.

## Как запустить свой workflow

Есть два варианта:

1. Прямо попросить: “use a workflow”, “run a workflow” или написать `ultracode: ...`.

Пример из доки:

```text
ultracode: audit every API endpoint under src/routes/ for missing auth checks
```

2. Включить режим:

```text
/effort ultracode
```

Ultracode = `xhigh reasoning effort` + автоматическая workflow orchestration.

Важно: в этом режиме Claude может делать несколько workflows подряд: например, один для понимания кода, второй для изменения, третий для проверки. Это дороже и дольше.

Откатиться обратно:

```text
/effort high
```

## Управление запуском

Команда `/workflows` показывает running/completed workflows.

В progress view видно:
- phases
- agent count
- token total
- elapsed time
- детали по каждому agent: prompt, recent tool calls, result

Горячие клавиши:
- `p` — pause/resume
- `x` — stop selected agent или весь workflow
- `r` — restart selected running agent
- `s` — save workflow script as command
- Enter/→ — drill down
- Esc — назад

## Сохранение workflow

Если workflow получился полезным, его можно сохранить как slash-command.

Локации:
- `.claude/workflows/` — внутри проекта, шарится с repo
- `~/.claude/workflows/` — личный глобальный workflow

Потом запускается как `/<name>`.

Если project workflow и personal workflow имеют одно имя — побеждает project workflow.

## Передача аргументов

Saved workflow может принимать `args`.

Пример из доки:

```text
Run /triage-issues on issues 1024, 1025, and 1030
```

Claude передаёт список как structured data, а скрипт читает глобальную переменную `args`.

То есть можно делать reusable workflows, например:
- `/audit-auth src/routes`
- `/review-issues [123, 456]`
- `/migration-plan {"from":"v1","to":"v2"}`

## Где лежат scripts

Каждый run пишет свой script в файл внутри `~/.claude/projects/`.

Claude получает путь к этому файлу при старте run. Его можно:
- открыть
- прочитать
- diff’нуть с прошлым запуском
- отредактировать
- попросить Claude перезапустить workflow из изменённой версии

## Ограничения runtime

Официальные лимиты:
- нет mid-run user input; только permission prompts могут остановить run. Если нужен human sign-off между этапами — делай этапы отдельными workflows.
- workflow script не имеет прямого filesystem/shell access. Скрипт координирует. Файлы читают/пишут и команды запускают agents.
- до 16 concurrent agents; на слабых машинах может быть меньше.
- до 1000 agents total per run; это защита от runaway loops.

## Resume

Workflow можно остановить и продолжить в той же Claude Code session.

Что уже завершилось — вернётся из cache, остальное запустится live.

Но если выйти из Claude Code, следующая session стартует workflow заново.

## Permissions

Subagents, которых запускает workflow, работают в режиме `acceptEdits` и наследуют твой tool allowlist.

- file edits auto-approved
- shell/web/MCP calls, которых нет в allowlist, могут спросить permission mid-run
- в `claude -p` и Agent SDK интерактивного подтверждения нет, поэтому всё зависит от настроенных permission rules

Для длинных workflow лучше заранее добавить нужные команды в allowlist, иначе run может застрять на prompt.

## Как отключить

Для себя: `/config`, или `{"disableWorkflows": true}` в `~/.claude/settings.json`, или env `CLAUDE_CODE_DISABLE_WORKFLOWS=1`.

Для организации — через managed settings или Claude Code admin settings.

## Практический вывод

Это фактически coded orchestration layer внутри Claude Code.

Раньше варианты были:
- основной Claude как orchestrator
- subagents
- skills
- agent teams
- внешний orchestrator типа Hermes/OpenClaw

Dynamic Workflows добавляют промежуточный уровень: Claude проектирует pipeline → runtime исполняет script → subagents работают пачками → результаты агрегируются без раздувания context window.

Для наших сценариев это особенно интересно для:
- массового аудита репозитория
- поиска auth/security gaps
- миграций по множеству файлов
- deep research по техдокам/рынку/инструментам
- генерации structured reports
- сравнения нескольких архитектурных вариантов
- QA сложных PR перед ревью человеком
```

## Краткая выжимка

Официальная документация уточняет, что Dynamic Workflows — это не просто «много субагентов», а JavaScript orchestration runtime в Claude Code: Claude пишет скрипт, runtime исполняет его в фоне, результаты агентов хранятся в переменных, а пользователь управляет run через `/workflows`. Важные операционные детали: `v2.1.154+`, `/deep-research`, `/effort ultracode`, сохранение в `.claude/workflows/` или `~/.claude/workflows/`, structured `args`, лимиты 16 concurrent agents и 1000 agents per run, отсутствие прямого shell/filesystem access у самого script, и permissions через `acceptEdits` + tool allowlist.
