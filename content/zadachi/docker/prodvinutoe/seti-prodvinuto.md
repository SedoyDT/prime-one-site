---
publish: true
title: "Задача: Docker-сети продвинуто: bridge/host/none, кастомные сети"
---

# Задача: Docker-сети продвинуто: bridge/host/none, кастомные сети

Создайте пользовательскую сеть `test-net`, запустите в ней контейнер `nginx` с именем `web`, затем запустите одноразовый контейнер `alpine` в той же сети, который через `wget -qO- http://web` проверит, что nginx отвечает по имени сервиса.

<details>
<summary>Решение</summary>

```bash
docker network create test-net

docker run -d --name web --network test-net nginx

docker run --rm --network test-net alpine wget -qO- http://web
# Выведет HTML стартовой страницы nginx — "web" разрешилось через встроенный DNS сети test-net
```

</details>
