---
publish: true
title: "Задача: Написать конфиг проекта на два окна"
---

# Задача: Написать конфиг проекта на два окна

Опишите tmuxinator-проект `demo` с двумя окнами: `editor` — разбитое на 2 панели (в одной ничего не запускать, во второй — `echo "watching"`), и `server` — одна панель, выполняющая `echo "server running"`. Запустите проект.

<details>
<summary>Решение</summary>

`~/.config/tmuxinator/demo.yml`:

```yaml
name: demo
root: ~/

windows:
  - editor:
      layout: main-vertical
      panes:
        -
        - echo "watching"
  - server:
      layout: main-vertical
      panes:
        - echo "server running"
```

Пустой элемент списка `panes:` (первая панель окна `editor`) — просто пустая панель с шеллом, без команды. Запуск:

```bash
tmuxinator start demo
```

должна подняться сессия `demo` с двумя окнами: `editor` (2 панели, вторая печатает `watching`) и `server` (1 панель, печатает `server running`).

</details>
