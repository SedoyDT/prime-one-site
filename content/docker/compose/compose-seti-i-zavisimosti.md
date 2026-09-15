---
publish: true
title: "Задача: Compose: сети и зависимости сервисов"
---

# Задача: Compose: сети и зависимости сервисов

Опишите два сервиса: `cache` (образ `redis:7-alpine`) и `worker` (собирается из `./worker`), где `worker` зависит от старта `cache` и подключается к нему по адресу `redis://cache:6379`.

<details>
<summary>Решение</summary>

```yaml
services:
  worker:
    build: ./worker
    environment:
      - REDIS_URL=redis://cache:6379
    depends_on:
      - cache

  cache:
    image: redis:7-alpine
```
Хост `cache` в `REDIS_URL` работает благодаря тому, что сервис назван именно `cache` — имя сервиса в YAML и есть его сетевое DNS-имя внутри compose-сети.

</details>
