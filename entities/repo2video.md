---
title: repo2video — видеопояснения кода из GitHub
created: 2026-10-11
updated: 2026-10-11
type: entity
tags: [agent, open-source, devtools, ai-engineering, automation, workflow]
sources: [raw/articles/repo2video-readme-2026-10-11.md]
confidence: medium
---

# repo2video

[repo2video](https://github.com/kuncevichandrew2/repo2video) — скилл для Claude Code, который по ссылке на GitHub-репозиторий готовит обучающее видео с объяснением архитектуры и ключевых участков кода. [Файл скилла](https://github.com/kuncevichandrew2/repo2video/blob/main/repo2video/SKILL.md) задаёт процедуру: клонировать и изучить проект, составить план «сначала архитектура, затем код», написать текст озвучки и подсказки к фрагментам кода, передать данные движку рендеринга.

## Что заявлено

- На выходе — MP4 1080p с подсветкой кода, деревом файлов, схемами Mermaid и речевым сопровождением.
- За анализ и сценарий отвечает Claude Code; [RepoTutor](https://github.com/kuncevichandrew2/repotutor) делает TTS и видеорендер через Remotion с резервным режимом FFmpeg.
- Для сценария скилла заявлена бесплатная Edge TTS без обязательного API-ключа; ElevenLabs — необязательная альтернатива. Базовые зависимости: Node.js 18+, Git, FFmpeg; первый запуск дополнительно устанавливает движок и браузер для Remotion.
- Пример запроса в Claude Code: `/repo2video https://github.com/owner/repo`. Скилл рассчитан на ролики длительностью 1–15 минут, по умолчанию 5 минут.

## Практическое применение и ограничения

Подходит для введения в чужую кодовую базу, объяснения архитектуры и подготовки учебного walkthrough. В отличие от скилла, который **только пишет сценарий**, здесь заявлен полный путь до MP4. Он связан с практиками [[agent-skills]] и [[agentic-coding-workflows]]: агент изучает реальные файлы, а визуализация и озвучка собираются по подготовленному им плану.

- Это **скилл Claude Code**, не готовая интеграция с Hermes; для применения в Hermes нужны адаптация инструкций и проверка совместимости движка.
- Репозиторий движка содержит также отдельный веб-сценарий, в README которого упоминаются ключи OpenRouter/ElevenLabs; заявление «без API-ключей» относится к описанному в скилле CLI-пути, а не ко всем режимам RepoTutor.
- README и `SKILL.md` изучены, но генерация видео не запускалась; итоговое качество и воспроизводимость на Linux не подтверждены. Перед использованием стороннего скилла проверить код, сетевые обращения и выполняемые команды.
- Язык озвучки по умолчанию — английский (`en-US-GuyNeural`); русский ролик потребует настройки голоса и проверки произношения технических терминов.

## Ссылки

- [Исходный README, сохранённый в базе](../raw/articles/repo2video-readme-2026-10-11.md)
- [SKILL.md на GitHub](https://github.com/kuncevichandrew2/repo2video/blob/main/repo2video/SKILL.md)
- [Движок RepoTutor](https://github.com/kuncevichandrew2/repotutor)

## Связанные страницы

- [[agent-skills]]
- [[agentic-coding-workflows]]
- [[ai-engineering]]
