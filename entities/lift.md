---
title: Lift
created: 2026-06-20
updated: 2026-06-20
type: entity
tags: [model, vision, data, open-source, devtools]
sources: [raw/articles/datalab-lift-document-structured-extraction-2026-06-20.md]
confidence: high
---

# Lift

`Lift` — open-source 9B vision-модель Datalab для извлечения структурированного JSON из PDF и изображений по заданной JSON Schema. Модель относится к классу инструментов [[document-structured-extraction]]: вместо свободного OCR-текста она должна возвращать объект, соответствующий схеме, с schema-constrained decoding для валидного и типизированного вывода.

## Ключевые факты

- Репозиторий: `datalab-to/lift`; пакет: `lift-pdf`; модель: `datalab-to/lift` на Hugging Face.
- Назначение: structured data extraction из PDFs/images, включая multi-page documents и значения, которые могут span pages.
- Контракт вывода: JSON объект по переданной JSON Schema.
- Режимы запуска: локальный HuggingFace backend и remote/vLLM server.
- Интерфейсы: Python API, CLI `lift_extract`, vLLM-команда `lift_vllm`, Schema Studio для создания и тестирования схем.

## Benchmark из README

В публичных материалах Datalab для своего benchmark указаны такие значения:

| Model | Size | Field accuracy | Full-document accuracy | Median latency |
| --- | ---: | ---: | ---: | ---: |
| Datalab API | — | 95.9% | 44.4% | 30.8s |
| Gemini Flash 3.5 | — | 91.3% | 40.0% | 28.1s |
| **Lift** | 9B | **90.2%** | 20.9% | 9.5s |
| Azure Content Understanding | — | 83.4% | 22.2% | 73.7s |
| NuExtract3 | 4B | 81.5% | 8.4% | 8.3s |
| Qwen3.5-9B | 9B | 76.3% | 24.0% | 16.8s |

Эти цифры нужно читать как результаты конкретного benchmark, а не универсальную гарантию качества: latency зависит от железа, сервера, параллелизма, размера документов и схемы.

## Практическое значение

Для [[ai-engineering]] Lift интересен тем, что превращает извлечение данных из документов в воспроизводимый schema-first workflow. Вместо ручной настройки OCR + LLM prompt + post-processing можно задавать JSON Schema и получать структурированный результат, который сразу подходит для pipeline, валидации, загрузки в БД или сравнения с эталоном. Это особенно полезно для invoices, forms, contracts, reports и внутренних документов, где важна не просто распознанная строка, а правильное поле в правильном типе.

## Caveats

- Open-source модель не включает verification/citations/features уровня Datalab API; в README у Datalab API отдельно указаны Citations + Verification.
- JSON Schema должна быть совместима со schema-constrained decoder: сложные конструкции вроде `anyOf`/`oneOf` и часть ограничений могут ослаблять гарантию.
- Для production-процессов нужно мерить не только field accuracy, но и full-document accuracy, ошибки пропусков, hallucinated fields, latency на своих PDF и стоимость GPU.

## Связанные страницы

- [[document-structured-extraction]]
- [[ai-engineering]]
- [[dynamic-workflows]]
