---
publish: true
title: "Задача: Порты и сеть: `-p`, `EXPOSE`"
---

# Задача: Порты и сеть: `-p`, `EXPOSE`

Запустите контейнер `nginx` так, чтобы он был доступен на хосте по порту `9000`, и проверьте curl'ом, что он отвечает.

<details>
<summary>Решение</summary>

```bash
docker run -d -p 9000:80 --name web3 nginx
curl localhost:9000
# Должен вернуться HTML-код стартовой страницы nginx ("Welcome to nginx!")
```

</details>
