# Примеры сообщений A2A

| Файл | Назначение |
|------|------------|
| [request-example.json](request-example.json) | Входящий JSON-RPC запрос в `inbox/` |
| [request-iteration-with-parent-id.json](request-iteration-with-parent-id.json) | Запрос **доработки**: новый **UUID** в **`id`**, предок в **`parent_id`** (Iteration Policy, `docs/SYSTEM_INSTRUCTIONS.md` §7) |
| [response-example.json](response-example.json) | Тело ответа §2.2; **всегда** сохраняется как `outbox/res_{id}.json` |
| [envelope-metadata-example.json](envelope-metadata-example.json) | Пример **`metadata.json`** внутри **опционального** конверта `outbox/{id}/` |

Полный регламент размещения: **`docs/SYSTEM_INSTRUCTIONS.md` §2.3**.
