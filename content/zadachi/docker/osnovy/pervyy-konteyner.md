---
publish: true
title: "Задача: Первый контейнер: `docker run`"
---

# Задача: Первый контейнер: `docker run`

Запустите контейнер с образом `alpine` (маленький Linux-дистрибутив) так, чтобы он выполнил команду `echo "Hello from container"` и сразу завершился, автоматически удалившись после этого.

<details>
<summary>Решение</summary>

```bash
docker run --rm alpine echo "Hello from container"
```
`alpine` — образ, `echo "Hello from container"` — команда, которая выполнится внутри контейнера вместо команды по умолчанию. После завершения `echo` процесс контейнера заканчивается, и благодаря `--rm` сам контейнер удаляется.

</details>
