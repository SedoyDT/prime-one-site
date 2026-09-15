---
publish: true
title: "Задача: Healthcheck и restart policy"
---

# Задача: Healthcheck и restart policy

Добавьте к сервису `web` (образ собирается из `.`, слушает порт 3000 с эндпоинтом `/health`) healthcheck, проверяющий этот эндпоинт каждые 15 секунд с таймаутом 5 секунд и 3 попытками, и restart policy `unless-stopped`.

<details>
<summary>Решение</summary>

```yaml
services:
  web:
    build: .
    ports:
      - "3000:3000"
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 15s
      timeout: 5s
      retries: 3
    restart: unless-stopped
```

</details>
