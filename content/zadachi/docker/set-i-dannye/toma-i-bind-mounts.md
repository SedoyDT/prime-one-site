---
publish: true
title: "Задача: Тома и bind mounts: хранение данных"
---

# Задача: Тома и bind mounts: хранение данных

Создайте volume с именем `notes-data`, запустите контейнер `alpine`, который запишет строку `"hello"` в файл `/data/note.txt` внутри тома, затем удалите контейнер и запустите новый с тем же volume, который прочитает и выведет содержимое файла.

<details>
<summary>Решение</summary>

```bash
docker volume create notes-data

docker run --rm -v notes-data:/data alpine sh -c 'echo hello > /data/note.txt'

docker run --rm -v notes-data:/data alpine cat /data/note.txt
# Вывод: hello
```
Оба запуска — разные, независимые контейнеры (первый уже удалён благодаря `--rm`), но данные сохранились, потому что они физически живут в volume `notes-data`, а не в файловой системе конкретного контейнера.

</details>
