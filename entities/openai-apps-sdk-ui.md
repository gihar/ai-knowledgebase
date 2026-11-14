---
title: OpenAI Apps SDK UI — дизайн-система для приложений внутри ChatGPT
created: 2026-11-14
updated: 2026-11-14
type: entity
tags: [open-source, product, devtools, ai-engineering]
sources: [raw/articles/openai-apps-sdk-ui-forwarded-2026-11-14.md, raw/articles/openai-apps-sdk-ui-readme-2026-11-14.md]
confidence: high
---

# OpenAI Apps SDK UI

[Apps SDK UI](https://github.com/openai/apps-sdk-ui) — открытая библиотека интерфейсных компонентов и дизайн-токенов OpenAI для **приложений ChatGPT, создаваемых с помощью Apps SDK**. Это не полный SDK и не готовый «плагин» с backend: библиотека отвечает за визуальный слой внутри ChatGPT. [README по фиксированному коммиту](../raw/articles/openai-apps-sdk-ui-readme-2026-11-14.md) описывает библиотеку как lightweight accessible design system; лицензия MIT.

## Возможности и применение

- Токены цвета, типографики, отступов, размеров, теней и поверхностей; интеграция с Tailwind 4, тёмный режим и адаптивная компоновка.
- React-компоненты с основой на Radix primitives и утилиты для согласованного интерфейса. В примере README используются `Button`, `Badge` и иконки в карточке бронирования; провайдер для ссылок необязателен.
- Установка: `npm install @openai/apps-sdk-ui`; требуются **React 18 или 19** и **Tailwind 4**. Нужно подключить стили и `@source` к пакету, чтобы Tailwind обнаружил классы компонентов.
- [Каталог компонентов](https://openai.github.io/apps-sdk-ui/) полезен при проектировании интерактивных карточек и других UI-поверхностей внутри ChatGPT. Из README нельзя сделать вывод, что подключение одной библиотеки автоматически создаёт и публикует приложение в ChatGPT: нужен отдельный Apps SDK-процесс и интеграция.

## Ограничения

В [пересланном сообщении](../raw/articles/openai-apps-sdk-ui-forwarded-2026-11-14.md) отдельно перечислены элементы чата и всплывающие подсказки. Проверенный README подтверждает библиотеку компонентов и адаптивные стили, но **не перечисляет эти два вида компонентов явно**; их наличие по конкретным именам/экспортам требует отдельной проверки каталога. Интеграция и работа внутри ChatGPT в этой вики не тестировались.

В отличие от [[astryx]] (дизайн-система общего назначения для React и coding-агентов), Apps SDK UI ориентирована на интерфейсы приложений ChatGPT. Как и [[agentic-frontend-stack|другие UI-библиотеки]], она не заменяет agent/backend-протокол, управление состоянием и авторизацию.

## Материалы

- [Репозиторий OpenAI](https://github.com/openai/apps-sdk-ui)
- [Сохранённый README](../raw/articles/openai-apps-sdk-ui-readme-2026-11-14.md)
- [Пересланное сообщение](../raw/articles/openai-apps-sdk-ui-forwarded-2026-11-14.md)

## Связанные страницы

- [[astryx]]
- [[agentic-frontend-stack]]
- [[ai-engineering]]
