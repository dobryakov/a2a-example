# A2A: файловая шина на Git (JSON-RPC 2.0)

Репозиторий задаёт среду обмена сообщениями **Agent-to-Agent** через файловую систему и **версионирование состояния через Git**.

## Структура

| Путь | Назначение |
|------|----------------|
| `inbox/` | Очередь входящих JSON-RPC запросов (статус **PENDING**) |
| `processing/` | Активные задачи (**LOCKED** — захваченные конкретным агентом) |
| `outbox/` | Готовые ответы (**COMPLETED**) |
| `archive/` | Архив обработанных запросов |
| `.well-known/agents/` | Манифесты агентов |
| `config/` | Конфигурация окружения (пути, версия протокола) |
| `docs/` | Спецификации и системные инструкции |

## Документы для агентов

1. **[docs/SYSTEM_INSTRUCTIONS.md](docs/SYSTEM_INSTRUCTIONS.md)** — формальные системные инструкции (рабочий цикл, инварианты, переходы состояний).
2. **[docs/ATOMIC_CAPTURE.md](docs/ATOMIC_CAPTURE.md)** — модель атомарного захвата задачи и исключение коллизий.
3. **[docs/VERSIONING.md](docs/VERSIONING.md)** — как Git фиксирует снимки состояния очередей и сообщений.

## Быстрый старт

- Манифест агента: `.well-known/agents/{agent_id}.json`.
- Шаблон роли **Data Analyst**: [.well-known/agents/data_analyst.json](.well-known/agents/data_analyst.json).
- Корневые пути задаются в `config/a2a-environment.json`.
