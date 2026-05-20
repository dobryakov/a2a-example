# A2A: файловая шина на Git (JSON-RPC 2.0)

Репозиторий задаёт среду обмена сообщениями **Agent-to-Agent** через файловую систему и **версионирование состояния через Git**.

## Структура

| Путь | Назначение |
|------|----------------|
| `inbox/` | Очередь входящих JSON-RPC запросов (статус **PENDING**) |
| `processing/` | Активные задачи (**LOCKED** — захваченные конкретным агентом) |
| `outbox/` | Готовые ответы (**COMPLETED**): **всегда** `res_{id}.*` с JSON-RPC телом §2.2; **опционально** каталог `{id}/` с вложениями и `metadata.json` (см. `docs/SYSTEM_INSTRUCTIONS.md` §2.3) |
| `archive/` | Архив обработанных запросов |
| `.well-known/agents/` | Манифесты агентов |
| `config/` | Конфигурация окружения (пути, версия протокола) |
| `docs/` | Спецификации и системные инструкции |

## Документы для агентов

1. **[PROTOCOL.md](PROTOCOL.md)** — короткий обзор протокола и ссылка на **Iteration Policy** (итерации и `parent_id`).
2. **[docs/SYSTEM_INSTRUCTIONS.md](docs/SYSTEM_INSTRUCTIONS.md)** — формальные системные инструкции (рабочий цикл, инварианты, переходы состояний, **паттерн Конверта** для `outbox/`, §2.3; **итерации — §7**). Примеры выдачи: **[docs/examples/README.md](docs/examples/README.md)**.
3. **[docs/ATOMIC_CAPTURE.md](docs/ATOMIC_CAPTURE.md)** — модель атомарного захвата задачи и исключение коллизий.
4. **[docs/VERSIONING.md](docs/VERSIONING.md)** — как Git фиксирует снимки состояния очередей и сообщений.

## Для помощников ИИ

- **[CLAUDE.md](CLAUDE.md)** — краткая навигация по инструкциям (таблица ссылок).
- Правило Cursor: [.cursor/rules/a2a-file-bus.mdc](.cursor/rules/a2a-file-bus.mdc) (`alwaysApply`).
- Claude-скилл «текст → `inbox/`»: [.claude/skills/a2a-task-from-text/SKILL.md](.claude/skills/a2a-task-from-text/SKILL.md).
- Claude-скилл исполнителя (`inbox/` → ответ): [.claude/skills/a2a-inbox-worker/SKILL.md](.claude/skills/a2a-inbox-worker/SKILL.md).

## Быстрый старт

- Манифест агента: `.well-known/agents/{agent_id}.json`.
- Шаблон роли **Data Analyst**: [.well-known/agents/data_analyst.json](.well-known/agents/data_analyst.json).
- Шаблон роли **Product Manager**: [.well-known/agents/product_manager.json](.well-known/agents/product_manager.json).
- Корневые пути задаются в `config/a2a-environment.json`.
