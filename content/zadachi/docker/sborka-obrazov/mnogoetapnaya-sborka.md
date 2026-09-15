---
publish: true
title: "Задача: Многоэтапная сборка (multi-stage build)"
---

# Задача: Многоэтапная сборка (multi-stage build)

Есть Go-программа `main.go`. Напишите multi-stage Dockerfile: на первом этапе (`golang:1.22`) скомпилируйте её в бинарник `app` (`go build -o app main.go`), на втором этапе используйте лёгкий базовый образ `alpine` и скопируйте туда только бинарник, запускайте его как команду по умолчанию.

<details>
<summary>Решение</summary>

```dockerfile
FROM golang:1.22 AS builder
WORKDIR /src
COPY main.go .
RUN go build -o app main.go

FROM alpine
WORKDIR /app
COPY --from=builder /src/app .
CMD ["./app"]
```
Финальный образ на базе `alpine` весит несколько мегабайт вместо примерно гигабайта, который занимает полный образ `golang`.

</details>
