---
publish: true
title: "Задача: Оптимизация размера образа"
---

# Задача: Оптимизация размера образа

Есть неоптимальный Dockerfile:
```dockerfile
FROM ubuntu:22.04
RUN apt-get update
RUN apt-get install -y python3 python3-pip
RUN apt-get clean
COPY . /app
WORKDIR /app
RUN pip3 install -r requirements.txt
CMD ["python3", "app.py"]
```
Перепишите его, применив минимум два приёма оптимизации из заметки.

<details>
<summary>Решение</summary>

```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
CMD ["python3", "app.py"]
```
Применено: (1) лёгкий специализированный базовый образ вместо `ubuntu` + ручная установка python; (2) `requirements.txt` копируется отдельно раньше остального кода — кэш зависимостей не слетает при правках кода; (3) `--no-cache-dir` у pip не оставляет кэш пакетов в слое.

</details>
