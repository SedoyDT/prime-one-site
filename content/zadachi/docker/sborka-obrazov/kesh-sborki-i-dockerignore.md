---
publish: true
title: "Задача: Кэш сборки, порядок инструкций, `.dockerignore`"
---

# Задача: Кэш сборки, порядок инструкций, `.dockerignore`

У вас Dockerfile для Python-приложения с `requirements.txt` и кодом в папке `app/`. Перепишите его так, чтобы изменение кода в `app/` не приводило к переустановке зависимостей.

<details>
<summary>Решение</summary>

```dockerfile
FROM python:3.12-slim
WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY app/ ./app/

CMD ["python", "app/main.py"]
```
`requirements.txt` копируется и ставится отдельным, более ранним слоем — он останется в кэше, пока сам файл зависимостей не изменится, независимо от правок в `app/`.

</details>
