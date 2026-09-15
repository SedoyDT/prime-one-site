---
publish: true
title: "Задача: Сборка образов: `docker build`, теги, слои"
---

# Задача: Сборка образов: `docker build`, теги, слои

У вас есть `Dockerfile` из предыдущей заметки (Python-скрипт) в папке `./myscript`. Соберите образ с именем `myscript` и тегом `v1`, затем запустите из него контейнер, который автоматически удалится после завершения.

<details>
<summary>Решение</summary>

```bash
docker build -t myscript:v1 ./myscript

docker run --rm myscript:v1
```
Контекст сборки — `./myscript` (там лежит `Dockerfile` и `app.py`), а не текущая директория, если запускать команду откуда-то ещё.

</details>
