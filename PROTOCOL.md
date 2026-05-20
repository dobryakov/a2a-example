# A2A Protocol (обзор)

Этот файл — **краткая входная точка** в нормативный протокол репозитория. Полная спецификация форматов, жизненного цикла задач и паттерна выдачи в `outbox/` находится в **[docs/SYSTEM_INSTRUCTIONS.md](docs/SYSTEM_INSTRUCTIONS.md)**.

## Ключевые темы

| Тема | Где подробности |
|------|------------------|
| JSON-RPC запрос (поля, в т.ч. **`parent_id`**) | `docs/SYSTEM_INSTRUCTIONS.md` §2.1 |
| Ответ, **`res_{id}.*`**, опциональный конверт **`outbox/{id}/`** | §2.2–2.3 |
| Захват задачи атомарным `rename` | [docs/ATOMIC_CAPTURE.md](docs/ATOMIC_CAPTURE.md) |
| Цикл **A→B→C→D**, Git **`Processed <id>`** | `docs/SYSTEM_INSTRUCTIONS.md` §3 |
| **Iteration Policy** — дерево итераций, базовый контекст, запрет перезаписи предков | **§7** того же документа |
| Git как журнал снимков | [docs/VERSIONING.md](docs/VERSIONING.md) |

## Iteration Policy (суть)

- Доработка оформляется **новым** `id` (рекомендуется **UUID v4**) и полем **`parent_id`**, указывающим на **непосредственного** предшественника.
- Исполнитель **обязан** загрузить базовый контекст из **`outbox/`** (и при необходимости из **`archive/`**) по **`parent_id`** до выполнения работы.
- Файлы выдачи и архива предка **не переписываются**; новая итерация публикует **`outbox/res_{новый_id}.*`** и при необходимости **новый** конверт **`outbox/{новый_id}/`**.

Пример запроса на доработку: **[docs/examples/request-iteration-with-parent-id.json](docs/examples/request-iteration-with-parent-id.json)**.
