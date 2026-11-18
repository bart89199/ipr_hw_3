### Запуск

```sh
docker compose -f task3/compose.yaml up -d
```

### Остановка

```sh
docker compose -f task3/compose.yaml down
```
### Проверка контейнеров

```sh
docker compose -f task3/compose.yaml ps
```

### Отчистить счётчик

```sh
docker compose -f task3/compose.yaml down -v
```

### Настройка портов и приветствия в `.env`

### Проверка

```sh
curl -fsS http://127.0.0.1:8000/
```
```sh
curl -fsS -X POST http://127.0.0.1:8000/increment
```
```sh
curl -fsS http://127.0.0.1:8000/readyz
```
```sh
curl -fsS http://127.0.0.1:8000/healthz
```

Или вместо 8000 порт, который вы указали в `.env`

### Проверка, что счётчик сохраняется после удаления и повторного создания контейнера

Запускаем контейнер

```sh
docker compose -f task3/compose.yaml up -d
```

Увеличиваем счётчик

```sh
curl -fsS -X POST http://127.0.0.1:8000/increment
curl -fsS -X POST http://127.0.0.1:8000/increment
curl -fsS -X POST http://127.0.0.1:8000/increment
```

Останавливаем и удаляем контейнер

```sh
docker compose -f task3/compose.yaml down
```

Запускаем контейнер снова

```sh
docker compose -f task3/compose.yaml up -d
```

Проверяем счётчик

```sh
curl -fsS http://127.0.0.1:8000/
```

Останавливаем и удаляем контейнер

```sh
docker compose -f task3/compose.yaml down
```

### Проверка, что происходит при выключении базы данных

Запускаем контейнер

```sh
docker compose -f task3/compose.yaml up -d
```

Увеличиваем счётчик

```sh
curl -fsS -X POST http://127.0.0.1:8000/increment
curl -fsS -X POST http://127.0.0.1:8000/increment
curl -fsS -X POST http://127.0.0.1:8000/increment
```

Останавливаем redis

```sh
docker compose -f task3/compose.yaml stop redis
```

Проверяем работу
```sh
curl -fsS http://127.0.0.1:8000/healthz
```

Проверяем ready
```sh
curl -fsS http://127.0.0.1:8000/readyz
```

Проверяем статус

```sh
docker compose -f task3/compose.yaml ps
```

Включаем redis

```sh
docker compose -f task3/compose.yaml start redis
```

Проверяем счётчик

```sh
curl -fsS http://127.0.0.1:8000/
```

Проверяем увеличение счётчика

```sh
curl -fsS -X POST http://127.0.0.1:8000/increment
curl -fsS -X POST http://127.0.0.1:8000/increment
curl -fsS -X POST http://127.0.0.1:8000/increment
```

Останавливаем и удаляем контейнер

```sh
docker compose -f task3/compose.yaml down
```