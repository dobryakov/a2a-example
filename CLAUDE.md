# Инструкции для ИИ (A2A-репозиторий)

Краткая навигация по документам протокола. **Перед правками очередей или добавлением JSON в `inbox/`, `processing/`, `outbox/`, `archive/` прочти нормативные файлы целиком.**

| Документ | Назначение |
|----------|------------|
| [docs/SYSTEM_INSTRUCTIONS.md](docs/SYSTEM_INSTRUCTIONS.md) | Формальные системные инструкции агента цикл захвата, обработки, финализации, Git и эскалация |
| [docs/ATOMIC_CAPTURE.md](docs/ATOMIC_CAPTURE.md) | Атомарное взятие задачи (`rename`), гонки, конфликты |
| [docs/VERSIONING.md](docs/VERSIONING.md) | Git как журнал неизменяемых «снимков» дерева сообщений |

| Прочее | Путь |
|--------|------|
| Обзор репозитория | [README.md](README.md) |
| Пути очередей и версия окружения | [config/a2a-environment.json](config/a2a-environment.json) |
| Манифесты агентов | [.well-known/agents/](.well-known/agents/) |
| Примеры JSON-RPC | [docs/examples/request-example.json](docs/examples/request-example.json), [docs/examples/response-example.json](docs/examples/response-example.json) |

Правило Cursor для этой работы см. [.cursor/rules/a2a-file-bus.mdc](.cursor/rules/a2a-file-bus.mdc).
