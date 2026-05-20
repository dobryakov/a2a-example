# Инструкции для ИИ (A2A-репозиторий)

Краткая навигация по документам протокола. **Перед правками очередей или добавлением JSON в `inbox/`, `processing/`, `outbox/`, `archive/` прочти нормативные файлы целиком.**

| Документ | Назначение |
|----------|------------|
| [PROTOCOL.md](PROTOCOL.md) | Краткий обзор протокола; ссылка на **Iteration Policy** (`SYSTEM_INSTRUCTIONS` §7) |
| [docs/SYSTEM_INSTRUCTIONS.md](docs/SYSTEM_INSTRUCTIONS.md) | Формальные системные инструкции: цикл захвата, обработки, финализации, Git, эскалация; **`outbox/`** — **всегда** `res_{id}.*`, конверт `{id}/` **опционален** (§2.3); **итерации и `parent_id` — §7** |
| [docs/ATOMIC_CAPTURE.md](docs/ATOMIC_CAPTURE.md) | Атомарное взятие задачи (`rename`), гонки, конфликты |
| [docs/VERSIONING.md](docs/VERSIONING.md) | Git как журнал неизменяемых «снимков» дерева сообщений |

| Прочее | Путь |
|--------|------|
| Обзор репозитория | [README.md](README.md) |
| Пути очередей и версия окружения | [config/a2a-environment.json](config/a2a-environment.json) |
| Манифесты агентов | [.well-known/agents/](.well-known/agents/) |
| Примеры и пояснения | [docs/examples/README.md](docs/examples/README.md) |

Правило Cursor для этой работы см. [.cursor/rules/a2a-file-bus.mdc](.cursor/rules/a2a-file-bus.mdc).

**Разделение ролей:** постановщик задачи и исполнитель очереди — это **разные** действия. Скилл «текст → `inbox/`» [.claude/skills/a2a-task-from-text/SKILL.md](.claude/skills/a2a-task-from-text/SKILL.md) **только** создаёт файл запроса в `inbox/` (или черновик). Он **не** должен в том же вызове выполнять работу воркера: не трогать `processing/`, не создавать `outbox/res_{id}.*` и конверт `outbox/{id}/`, не переносить запрос в `archive/`. Если нужен ответ в конверте или иной формат выдачи — опиши это в **`params`** запроса; выполнит отдельный прогон [.claude/skills/a2a-inbox-worker/SKILL.md](.claude/skills/a2a-inbox-worker/SKILL.md) (или другой явно задействованный исполнитель).

Черновик Claude-скилла «текст → задача в `inbox/`» см. [.claude/skills/a2a-task-from-text/SKILL.md](.claude/skills/a2a-task-from-text/SKILL.md).

Черновик скилла исполнителя (воркер `inbox/`) см. [.claude/skills/a2a-inbox-worker/SKILL.md](.claude/skills/a2a-inbox-worker/SKILL.md).
