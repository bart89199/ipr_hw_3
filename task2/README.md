### Запуск

```sh
docker compose -f task2/compose.yaml up -d
```

### Остановка

```sh
docker compose -f task2/compose.yaml down
```

### Отчистить счётчик

```sh
docker compose -f task2/compose.yaml down -v
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
docker compose -f task2/compose.yaml up -d
```

Увеличиваем счётчик

```sh
curl -fsS -X POST http://127.0.0.1:8000/increment
curl -fsS -X POST http://127.0.0.1:8000/increment
curl -fsS -X POST http://127.0.0.1:8000/increment
```

Останавливаем и удаляем контейнер

```sh
docker compose -f task2/compose.yaml down
```

Запускаем контейнер снова

```sh
docker compose -f task2/compose.yaml up -d
```

Проверяем счётчик

```sh
curl -fsS http://127.0.0.1:8000/
```

Останавливаем и удаляем контейнер

```sh
docker compose -f task2/compose.yaml down
```