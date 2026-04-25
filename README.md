Сборка и запуск

```bash
docker compose up --build
```

Остановка

```bash
docker compose down
```

Остановка с удалением volume

```bash
docker compose down -v
```

Проверка контейнеров

```bash
docker compose ps
```

Логи

```bash
docker compose logs -f
```

Масштабирование backend

```bash
docker compose up --build --scale backend=2
```
