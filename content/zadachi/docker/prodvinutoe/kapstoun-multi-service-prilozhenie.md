---
publish: true
title: "Задача: Капстоун: контейнеризация multi-service приложения"
---

# Задача: Капстоун: контейнеризация multi-service приложения

Проверьте себя на модификации: добавьте к этому проекту redis-кэш (образ `redis:7-alpine`) без внешнего порта, доступный сервису `backend` по адресу `redis://cache:6379`, и добавьте ему `restart: unless-stopped`. Задача — только сформулировать нужные изменения `docker-compose.yml` (не запускать реально).

<details>
<summary>Решение</summary>

Добавить сервис:
```yaml
  cache:
    image: redis:7-alpine
    restart: unless-stopped
```
И добавить в `backend` переменную окружения, ссылающуюся на него по имени сервиса:
```yaml
  backend:
    build: ./backend
    environment:
      - DATABASE_URL=postgres://postgres:${POSTGRES_PASSWORD}@db:5432/${POSTGRES_DB}
      - REDIS_URL=redis://cache:6379
    depends_on:
      db:
        condition: service_healthy
    restart: on-failure:3
```
Порт у `cache` не пробрасывается — как и `db`, он доступен только внутри сети compose, по имени сервиса, для других контейнеров этого проекта.

</details>
