---
publish: true
title: "Задача: Dockerfile: основы (FROM, RUN, COPY, CMD)"
---

# Задача: Dockerfile: основы (FROM, RUN, COPY, CMD)

Напишите `Dockerfile` для простого Python-скрипта: базовый образ `python:3.12-slim`, рабочая директория `/app`, копируется файл `app.py`, команда запуска — `python app.py`.

<details>
<summary>Решение</summary>

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY app.py .

CMD ["python", "app.py"]
```
Для одного файла без внешних зависимостей отдельный шаг `RUN pip install` не нужен — `COPY` и `CMD` достаточно.

</details>
