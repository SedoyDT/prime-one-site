---
publish: true
title: "Задача: Безопасность контейнеров: non-root, secrets"
---

# Задача: Безопасность контейнеров: non-root, secrets

В следующем Dockerfile есть две проблемы безопасности из разобранных в заметке. Найдите и исправьте обе.
```dockerfile
FROM node:20-alpine
ENV API_SECRET=sk_live_abc123xyz
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "server.js"]
```

<details>
<summary>Решение</summary>

Проблемы: (1) секрет `API_SECRET` зашит прямо в образ через `ENV` — виден всем, у кого есть образ, и остаётся в слое навсегда, даже если позже удалить эту строку в новой версии; (2) отсутствует непривилегированный пользователь — контейнер работает от root.
```dockerfile
FROM node:20-alpine
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
WORKDIR /app
COPY --chown=appuser:appgroup . .
RUN npm install
USER appuser
CMD ["node", "server.js"]
```
Секрет `API_SECRET` теперь передаётся при запуске: `docker run -e API_SECRET=sk_live_abc123xyz myapp` (а ещё лучше — из `--env-file`, не попадающего в историю shell).

</details>
