# Docker-контейнеризация приложения

## Состав проекта

- `backend` — backend на Go
- `frontend` — frontend на Vue.js

## Используемые технологии

- Docker
- Docker Compose
- Multi-stage builds
- Go + Alpine
- Vue.js + Nginx Unprivileged

## Особенности контейнеризации

### Backend
- Собирается через multi-stage build
- На этапе сборки используется `golang:1.22-alpine`
- Финальный образ основан на `alpine:3.20`
- Приложение запускается от непривилегированного пользователя
- Присутствует healthcheck: `/health`

### Frontend
- Собирается через multi-stage build
- На этапе сборки используется `node:16-alpine`
- Финальный образ основан на `nginxinc/nginx-unprivileged:1.27-alpine`
- Для production-сборки используется `VUE_APP_API_URL`
- Контейнер запускается без root

## Запуск проекта

Сборка и запуск:

```bash
docker compose up --build
```

После запуска приложение доступно по адресам:

Frontend: http://localhost
Backend: http://localhost:8081
Backend healthcheck: http://localhost:8081/health

Остановка
```bash
docker compose down
```

Остановка с удалением volume:

```bash
docker compose down -v
```

Проверка состояния контейнеров

```bash
docker compose ps
```

Просмотр логов
```bash
docker compose logs -f
```
Масштабирование backend
```bash
docker compose up --build --scale backend=2
```
