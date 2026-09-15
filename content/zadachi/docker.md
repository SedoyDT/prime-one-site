---
publish: true
title: "Docker: задачи для практики"
---

# Docker: задачи для практики

Набор коротких задач по Docker — от контейнеров и образов до healthcheck, безопасности и многосервисного compose-проекта. Решение — под спойлером.

## Основы: контейнеры, образы, Dockerfile

- [[docker_osnovy_chto-takoe-docker|Что такое Docker и зачем он нужен]]
- [[docker_osnovy_pervyy-konteyner|Первый контейнер: `docker run`]]
- [[docker_osnovy_obrazy-i-zhiznenny-cikl|Образы и контейнеры: жизненный цикл]]
- [[docker_osnovy_osnovnye-komandy-cli|Основные команды CLI (logs, exec, stop, rm)]]
- [[docker_osnovy_dockerfile-osnovy|Dockerfile: основы (FROM, RUN, COPY, CMD)]]
- [[docker_osnovy_sborka-obrazov-i-tegi|Сборка образов: `docker build`, теги, слои]]

## Сеть и данные

- [[docker_set-i-dannye_porty-i-set-osnovy|Порты и сеть: `-p`, `EXPOSE`]]
- [[docker_set-i-dannye_peremennye-okruzheniya|Переменные окружения и `.env`]]
- [[docker_set-i-dannye_toma-i-bind-mounts|Тома и bind mounts: хранение данных]]

## Продвинутая сборка образов

- [[docker_sborka-obrazov_kesh-sborki-i-dockerignore|Кэш сборки, порядок инструкций, `.dockerignore`]]
- [[docker_sborka-obrazov_mnogoetapnaya-sborka|Многоэтапная сборка (multi-stage build)]]

## Docker Compose

- [[docker_compose_docker-compose-osnovy|Docker Compose: основы, `docker-compose.yml`]]
- [[docker_compose_compose-seti-i-zavisimosti|Compose: сети и зависимости сервисов]]
- [[docker_compose_compose-tomy-i-env|Compose: тома и переменные окружения в проекте]]

## Надёжность и безопасность

- [[docker_nadezhnost-i-bezopasnost_logi-i-otladka|Логи и отладка: logs, exec, inspect, stats]]
- [[docker_nadezhnost-i-bezopasnost_healthcheck-i-restart-policy|Healthcheck и restart policy]]
- [[docker_nadezhnost-i-bezopasnost_optimizaciya-razmera-obraza|Оптимизация размера образа]]
- [[docker_nadezhnost-i-bezopasnost_bezopasnost-konteynerov|Безопасность контейнеров: non-root, secrets]]

## Продвинутые темы

- [[docker_prodvinutoe_seti-prodvinuto|Docker-сети продвинуто: bridge/host/none, кастомные сети]]
- [[docker_prodvinutoe_vvedenie-v-orkestraciyu|Введение в оркестрацию: зачем Swarm/Kubernetes]]
- [[docker_prodvinutoe_kapstoun-multi-service-prilozhenie|Капстоун: контейнеризация multi-service приложения]]
