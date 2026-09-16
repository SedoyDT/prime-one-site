---
publish: true
title: "tmuxinator: описываем окружение проекта в YAML"
---

# tmuxinator: описываем окружение проекта в YAML

Уровень сложности: ~25/100.

**Предполагается:** tmux и его биндинги — [[tmux-i-oh-my-tmux|установка tmux и конфиг oh-my-tmux]]. Дальше — [[scenarii-primeneniya-tmux-tmuxinator|сценарии использования]].

## Проблема, которую решает tmuxinator

Каждое утро — одна и та же ручная последовательность: открыть tmux, создать окно под редактор, разбить его на панели, создать окно под сервер, окно под логи. tmuxinator описывает это один раз в YAML-файле и дальше поднимает всё одной командой.

## Установка

```bash
gem install tmuxinator
```

tmuxinator — Ruby-гем, для установки нужен Ruby с `gem` в PATH.

## Создание проекта

```bash
tmuxinator new myproject
```

Открывает `~/.config/tmuxinator/myproject.yml` в редакторе (или создаёт болванку). Базовые поля:

```yaml
name: myproject
root: ~/

windows:
  - editor:
      layout: main-vertical
```

`name` — имя проекта (и имя итоговой tmux-сессии), `root` — рабочая директория по умолчанию для всех панелей, `windows` — список окон.

## Наполняем окна панелями

```yaml
windows:
  - editor:
      layout: main-vertical
      panes:
        - nvim
        - guard
  - server:
      layout: main-vertical
      panes:
        - echo "server pane 1"
        - echo "server pane 2"
```

Каждый элемент `windows` — `имя-окна: {layout, panes}`. `layout` принимает именованные tmux-раскладки (`main-vertical`, `even-horizontal`, ...) или сырую tmux-команду сплита строкой. `panes` — список команд, каждая запускается в своей панели; элемент без команды — просто пустая панель с шеллом.

## Полезные опции (реально поддерживаются, не все обязательны)

```yaml
startup_window: editor   # какое окно получает фокус при старте
startup_pane: 1           # какая панель этого окна получает фокус
attach: false              # собрать сессию, но не прицепляться к ней сразу
tmux_options: -f ~/.tmux.mac.conf   # свой tmux.conf только для этого проекта
socket_name: foo           # изолированный tmux-сокет для проекта
```

## Хуки проекта

```yaml
on_project_start: echo "стартуем проект"
on_project_first_start: echo "первый запуск этого проекта"
on_project_restart: echo "перезапуск"
on_project_exit: echo "отцепились от сессии"
on_project_stop: echo "проект остановлен"
pre_window: rbenv shell 2.0.0-p247
```

`pre_window` выполняется в каждом окне/панели **перед** их собственной командой — удобно для вещей вроде переключения версии интерпретатора, которые иначе пришлось бы дублировать в каждой панели отдельно.

Более тонкий контроль — отдельный `hooks.sh`, где функции `pre_<имя-окна>`/`post_<имя-окна>` выполняются вокруг создания конкретного окна:

```bash
#!/bin/bash

# Для выполнения действий перед созданием окна
pre_my_window() {
  echo "Before Window"
}

# Для выполнения действий после создания окна
post_my_window() {
  echo "After Window"
}
```

## Команды

```bash
tmuxinator start myproject   # поднять всё описанное в yml
tmuxinator open myproject    # открыть yml на редактирование
tmuxinator list               # список всех проектов
tmuxinator stop myproject     # остановить сессию
tmuxinator delete myproject   # удалить конфиг проекта
```

## Проверка себя

Опишите проект с двумя окнами: `editor` (разбитое на 2 панели) и `server` (одна панель с любой долгоживущей командой, например `ping localhost`), поднимите его через `tmuxinator start`, убедитесь, что обе панели `editor` и панель `server` появились как описано, затем `tmuxinator stop`.

## Что дальше

[[scenarii-primeneniya-tmux-tmuxinator|tmux и tmuxinator: сценарии использования]] — те же команды в виде конкретных рабочих ситуаций.
