---
publish: true
title: "Задача: Compose: тома и переменные окружения в проекте"
---

# Задача: Compose: тома и переменные окружения в проекте

Опишите сервис `db` (образ `mysql:8`) с паролем root, читаемым из `.env`-переменной `MYSQL_ROOT_PASSWORD`, и именованным томом `mysql-data`, смонтированным в `/var/lib/mysql`.

<details>
<summary>Решение</summary>

`.env`:
```
MYSQL_ROOT_PASSWORD=rootpass
```
`docker-compose.yml`:
```yaml
services:
  db:
    image: mysql:8
    environment:
      - MYSQL_ROOT_PASSWORD=${MYSQL_ROOT_PASSWORD}
    volumes:
      - mysql-data:/var/lib/mysql

volumes:
  mysql-data:
```

</details>
