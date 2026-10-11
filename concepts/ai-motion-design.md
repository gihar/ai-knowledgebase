---
title: AI-моушн-дизайн — выбор инструментов по типу видео
created: 2026-10-11
updated: 2026-10-11
type: concept
tags: [agent, tool-use, workflow, automation, devtools, ai-engineering, open-source]
sources: [raw/articles/motion-design-15-repos-forwarded-2026-10-11.md]
confidence: medium
---

# AI-моушн-дизайн: подборка 15 репозиториев

Пересланная подборка различает **анимацию сайта** и **готовое видео**, а для видео предлагает выбирать между монтажом своего материала, презентационным роликом и короткой анимацией. Это каталог ориентиров для выбора, а не подтверждение, что все 15 проектов являются устанавливаемыми скиллами или работают с любой моделью без настройки. Схема выбора сохранена в [исходном посте](../raw/articles/motion-design-15-repos-forwarded-2026-10-11.md).

## Быстрый выбор

| Задача | Репозитории из подборки |
|---|---|
| Ролик для запуска продукта | [product-launch-motion](https://github.com/AbubakrChan/product-launch-motion), [motion-graphics-skills](https://github.com/charlie947/motion-graphics-skills), [claude-motion-design](https://github.com/howseen-ai/claude-motion-design) |
| Монтаж отснятого видео | [hyperframes-student-kit](https://github.com/nateherkai/hyperframes-student-kit), [motion-graphics](https://github.com/Barty-Bart/motion-graphics) |
| Короткий анимационный ролик | [animate](https://github.com/cth9191/animate), [claude-motion](https://github.com/whaleyxbt/claude-motion), [claude-remotion-skill](https://github.com/haidrrrry/claude-remotion-skill) |
| Анимация элементов сайта, не отдельный MP4 | [motion](https://github.com/motiondivision/motion), [motion-dev-animations-skill](https://github.com/199-biotechnologies/motion-dev-animations-skill) |

**Строительные блоки:** [HyperFrames](https://github.com/heygen-com/hyperframes) для HTML/CSS-анимации и рендера видео, [Remotion](https://github.com/remotion-dev/remotion) для программного видео на React, [Remotion Skills](https://github.com/remotion-dev/skills) как агентные инструкции, [GSAP Skills](https://github.com/greensock/gsap-skills) для анимации GSAP, [motion-design-skill](https://github.com/LottieFiles/motion-design-skill) с принципами движения. Формулировки назначения здесь пересказывают пост, а не результаты испытаний.

## Практические границы

- Все 15 указанных адресов GitHub отвечали через GitHub API на 11.10.2026; содержимое, статус «официальности», возможности, лицензии и безопасность каждого проекта отдельно не проверялись.
- Репозиторий библиотеки, агентный `SKILL.md` и стартовый набор для проекта — разные вещи: нельзя считать все позиции одним типом установки.
- Иллюстрация направляет ветку *web animation* к результату «live on your site», а три ветки видео — к MP4; она **не** утверждает, что `motion` сам экспортирует MP4.
- Перед установкой проверить README, `SKILL.md`, зависимости, разрешения и сетевые вызовы; протестировать на небольшом ролике. Общие критерии выбора и безопасности скиллов — в [[agent-skills]].
- Для обучающего видео именно **по коду GitHub-репозитория** см. [[repo2video]]; для работы со звуковой дорожкой готового видео — [[ai-video-dubbing]].

## Связанные страницы

- [[agent-skills]]
- [[repo2video]]
- [[ai-video-dubbing]]
- [[ai-engineering]]
