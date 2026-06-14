---
title: Fish Speech
created: 2026-06-14
updated: 2026-06-14
type: entity
tags: [tts, voice-cloning, speech-generation, local-ai, multimodal-audio]
sources: [raw/articles/fish-speech-local-russian-voice-cloning-2026-06-14.md]
confidence: medium
---

# Fish Speech

Fish Speech — open-source TTS/voice-cloning проект от Fish Audio. Репозиторий позиционирует Fish Audio S2/S2 Pro как multilingual text-to-speech систему с command-line, WebUI и server inference, быстрым voice cloning по коротким образцам и управлением просодией/эмоциями через текстовые инструкции.

## Практическая ценность

По пользовательскому опыту, [[fish-speech]] «более-менее нормально» справляется с русским языком и voice cloning, работает локально на M4 GPU и требует подбора настроек, как и другие нейросетевые модели. Главная ценность — локальная генерация речи без зависимости от платного баланса сервисов вроде ElevenLabs.

## Использование в workflow

Наиболее полезный сценарий — CLI-обвязка для [[ai-video-dubbing]]: агент или Codex skill получает команду «переозвучь», извлекает/получает текст, генерирует новую дорожку голосом через Fish Speech и собирает видео обратно. Это превращает TTS из разовой ручной операции в воспроизводимый AI-инжиниринговый pipeline.

## Ограничения и вопросы

- Качество русского и клонирования голоса требует ручной настройки и прослушивания результата.
- Локальная производительность зависит от железа, backend и выбранной модели.
- Лицензия проекта — Fish Audio Research License; перед коммерческим применением нужно отдельно проверить ограничения.
- Voice cloning и переозвучка требуют явного контроля прав на голос, исходные материалы и публикацию результата.

## Связанные страницы

- [[ai-video-dubbing]]
- [[ai-engineering]]
- [[agentic-coding-workflows]]
