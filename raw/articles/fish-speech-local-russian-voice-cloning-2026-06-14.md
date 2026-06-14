---
title: Fish Speech для локального TTS, voice cloning и переозвучки видео
source_url: telegram-forwarded-post
source_links:
  - https://github.com/fishaudio/fish-speech
ingested: 2026-06-14
sha256: 4776a0b7646875cd0d9e19f37f94fead4b59404855ecf90cd86a7700c779c612
type: raw
---

# Fish Speech для локального TTS, voice cloning и переозвучки видео

## Исходный текст

Игрался со свободными TTS моделями (генераторы речи). Рекомендую https://github.com/fishaudio/fish-speech — более менее норм справляется с войс клонингом и русским языком. Не идеально, но где вообще идеально.

Работает на M4 GPU локально. И нужно играться с настройками, как и для любых других сеток.
Зато свое, и не надо за балансом в eleven labs следить.

Для чего? Засуну в виде CLI в скилл кодекса, и когда нужно будет видосик переозвучить просто скажу переозвучь, и он сделает. Сейчас так сабы накладываю, а можно будет и вообще все подряд.

## Краткое описание

Заметка фиксирует практическую рекомендацию использовать [[fish-speech]] как свободную TTS/voice-cloning модель для русского языка. Важный workflow-мотив — обернуть модель в CLI и подключить к Codex skill, чтобы команда вроде «переозвучь видео» запускала весь pipeline переозвучки без зависимости от баланса ElevenLabs.

## Проверка источника

Репозиторий fishaudio/fish-speech описывает проект как open-source TTS. README указывает на Fish Audio S2/S2 Pro, multilingual TTS, command-line/server/WebUI inference, voice cloning from short samples и исследовательскую лицензию Fish Audio Research License. Практические утверждения о качестве русского языка и работе на M4 GPU в этой заметке являются пользовательским опытом и не были независимо воспроизведены при ingest.
