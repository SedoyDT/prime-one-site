---
publish: true
title: "Vim и LazyVim: от основ к LazyVim"
---

# Vim и LazyVim: от основ к LazyVim

Шесть туториалов по возрастанию сложности — от режимов и `hjkl` (уровень ~5) до устройства конфига LazyVim изнутри (уровень ~40). Голый Vim работает одинаково на любой системе, поэтому основы (00–39) не привязаны ни к какому дистрибутиву; установка LazyVim (40+) — осознанный следующий шаг после того, как движения и операторы уже в руках, а не замена им.

Сценарии применения на практике — [[scenarii-primeneniya-vim-lazyvim|Vim и LazyVim: сценарии использования]]. Короткие задачи с решением под спойлером — [[vim|Vim и LazyVim: задачи для практики]].

## 00–09 · Основы

- [[rezhimy-i-navigaciya|Режимы Vim и базовая навигация]] — Normal/Insert/Visual, `hjkl`, `w`/`e`/`b`, `d$`.

## 10–19 · Редактирование

- [[operatory-tochka-makrosy-registry|Редактирование: операторы, точка-повтор, макросы и регистры]] — `x`/`dd`, `cw`, `.`, `u`/`Nu`, макросы, именованные регистры.

## 20–29 · Поиск и замена

- [[poisk-i-substitute|Поиск и замена: `/pattern` и `:%s`]] — `/pattern`+`n`, `:%s/old/new/g`, замена в диапазоне строк.

## 30–39 · Многозадачность

- [[bufery-okna-vkladki|Буферы, окна и вкладки: многозадачность внутри Vim]] — buffer vs window, `:split`/`:vsplit`, `:b <имя>`.

## 40–49 · Установка LazyVim

- [[neovim-i-lazyvim-s-nulya|Установка Neovim и LazyVim с нуля]] — Homebrew, `neovim`/`ripgrep`/`fzf`, LazyVim starter, `:LazyHealth`, `:Mason`.

## 50–59 · LazyVim изнутри

- [[konfig-plaginy-lsp-format|LazyVim изнутри: свои плагины, LSP, форматирование и keymaps]] — `lua/plugins/`, `opts` vs `config`, `:LazyExtras`, LSP/Mason/conform/nvim-lint, живой пример своего keymap.
