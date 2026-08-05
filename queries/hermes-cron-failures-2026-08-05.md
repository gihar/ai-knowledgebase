---
title: Какие cron-задачи Hermes не выполнились 05.08.2026
created: 2026-08-05
updated: 2026-08-05
type: query
tags: [agent, workflow, automation, monitoring, incident]
sources: [raw/articles/hermes-cron-failures-2026-08-05.md]
confidence: high
---

# Какие cron-задачи Hermes не выполнились 05.08.2026

На момент проверки неуспешно завершились шесть cron-запусков. У всех одна причина: токен Codex не удалось обновить, поэтому агентная часть задач не стартовала.

## Реальные пропуски результата

- `markirovka-master-daily-normative-scan` — не собраны мастер-данные мониторинга.
- `markirovka-pro-daily-normative-monitoring` — не сформирован публичный пост, зависящий от master-результата.
- `chestny-znak-daily-critical-watch` — не сформирован внутренний PDF.
- `Синхронизация Smartsheet SEARCH-13164` — не выполнены синхронизация и проверка данных.

## Технические ошибки без ожидаемой публикации

- `mc-releases-pim-daily` получил 0 релизов и должен был завершиться `[SILENT]`.
- `reg-mon` получил `[SILENT]` от пре-чека и также не должен был отправлять отчёт.

## Восстановление

Сначала требуется повторная аутентификация Codex через `hermes model`. После этого приоритетно повторяются мониторинг маркировки (master → downstream) и синхронизация Smartsheet.

## Связи

- [[ai-agent-orchestration]]
- [[agent-looping]]
- [[agentic-coding-workflows]]
- [[ai-engineering]]
