---
publish: true
title: "Задача: Основные команды CLI (logs, exec, stop, rm)"
---

# Задача: Основные команды CLI (logs, exec, stop, rm)

Запустите `nginx` в фоне с именем `web2`, зайдите внутрь через `exec` и командой `cat` выведите содержимое файла `/etc/nginx/nginx.conf`, затем выйдите и остановите+удалите контейнер одной командой.

<details>
<summary>Решение</summary>

```bash
docker run -d --name web2 nginx

docker exec web2 cat /etc/nginx/nginx.conf
# (exec с командой сразу, без -it — не нужен интерактивный терминал для одной команды)

docker rm -f web2
# -f сначала останавливает (kill), потом удаляет — одна команда вместо stop + rm
```

</details>
