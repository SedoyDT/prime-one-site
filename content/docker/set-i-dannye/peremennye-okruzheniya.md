---
publish: true
title: "Задача: Переменные окружения и `.env`"
---

# Задача: Переменные окружения и `.env`

Создайте файл `.env` с двумя переменными `APP_MODE=test` и `PORT=3000`, запустите контейнер `alpine` с этим файлом и командой, которая выводит обе переменные.

<details>
<summary>Решение</summary>

Файл `.env`:
```
APP_MODE=test
PORT=3000
```
Команда:
```bash
docker run --rm --env-file .env alpine sh -c 'echo $APP_MODE $PORT'
# Вывод: test 3000
```

</details>
