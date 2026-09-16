---
publish: true
title: "Healthcheck, restart policy и отладка"
---

# Healthcheck, restart policy и отладка

Уровень сложности: ~75/100. Нужен установленный Docker.

**Предполагается:** знание `docker run`/`docker compose up` и что `depends_on` ждёт только запуска контейнера, а не готовности сервиса — см. [[docker-compose-ot-nulya|Docker Compose с нуля]].

## "Работает" ≠ "здоров"

Контейнер может быть в статусе `running`, пока процесс внутри него завис или база данных внутри ещё не приняла первое соединение. Docker по умолчанию не умеет отличать «жив» от «здоров» — только «процесс всё ещё исполняется». `HEALTHCHECK` в Dockerfile закрывает этот разрыв.

```dockerfile
FROM nginx:alpine
HEALTHCHECK --interval=10s --timeout=3s --retries=3 \
  CMD wget -q --spider http://localhost/ || exit 1
```

- `--interval=10s` — как часто проверять;
- `--timeout=3s` — сколько ждать ответа проверки, прежде чем считать её проваленной;
- `--retries=3` — сколько провалов подряд нужно, чтобы пометить контейнер `unhealthy`;
- команда после `CMD` — что именно проверяется; ненулевой код выхода = проверка провалена.

Соберите и запустите, затем понаблюдайте за статусом:

```
docker build -t health-demo .
docker run -d --name hc health-demo
docker ps
```

Столбец `STATUS` в `docker ps` через несколько секунд покажет `(healthy)` рядом с `Up`. Проверить состояние явно:

```
docker inspect --format='{{.State.Health.Status}}' hc
```

## Healthcheck в Compose

```yaml
services:
  db:
    image: postgres:16-alpine
    environment:
      - POSTGRES_PASSWORD=demo
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 5s
      timeout: 3s
      retries: 5

  app:
    image: alpine
    command: sleep 3600
    depends_on:
      db:
        condition: service_healthy
```

`depends_on` с `condition: service_healthy` — это исправление проблемы из прошлого туториала: `app` теперь стартует не когда контейнер `db` просто запущен, а когда его `HEALTHCHECK` впервые вернул успех, то есть Postgres реально готов принимать подключения.

## Restart policy: самовосстановление

По умолчанию упавший контейнер остаётся упавшим:

```
docker run -d --name flaky alpine sh -c "sleep 2; exit 1"
sleep 3
docker ps -a
```

`STATUS` покажет `Exited (1)`. Добавление политики перезапуска меняет поведение:

```
docker run -d --name flaky2 --restart unless-stopped alpine sh -c "sleep 2; exit 1"
sleep 10
docker ps -a
```

`COUNT` перезапусков будет расти — Docker сам поднимает контейнер заново после каждого падения. Варианты политики:

- **`no`** (по умолчанию) — никогда не перезапускать;
- **`on-failure[:N]`** — перезапускать только при ненулевом коде выхода, максимум N раз;
- **`unless-stopped`** — перезапускать всегда, кроме случая, когда контейнер остановлен явно (`docker stop`), в том числе переживает перезагрузку демона;
- **`always`** — перезапускать всегда, включая ручную остановку — при следующем старте демона Docker контейнер снова поднимется.

Уборка: `docker rm -f flaky flaky2`.

## Набор команд для отладки

Когда что-то работает не так, порядок действий обычно такой:

```
docker ps -a                     # жив ли контейнер вообще, какой код выхода
docker logs --tail 50 -f <name>   # последние строки и продолжение в реальном времени
docker inspect <name>              # вся метаинформация: сети, тома, переменные, healthcheck
docker stats <name>                # CPU/память/сеть в реальном времени
docker exec -it <name> sh           # зайти внутрь и посмотреть руками
```

`docker inspect` возвращает большой JSON — на практике почти всегда используется с `--format` для конкретного поля (как в примере с `Health.Status` выше) или в связке с `jq`.

## Проверка себя

Возьмите `health-demo` из начала туториала, временно остановите nginx внутри контейнера (`docker exec hc nginx -s stop`) и понаблюдайте через `docker ps`/`docker inspect`, как статус меняется на `unhealthy` — без перезапуска контейнера, потому что `HEALTHCHECK` сам по себе не перезапускает, а только сигнализирует. Автоматический перезапуск при `unhealthy` — задача внешнего оркестратора или отдельного скрипта-наблюдателя, к этому подводит следующий уровень.

## Что дальше

[[zashchita-konteynerov|Безопасность контейнеров]] — контейнер теперь наблюдаем и самовосстанавливается; следующий вопрос — что он может сломать, если скомпрометирован.
