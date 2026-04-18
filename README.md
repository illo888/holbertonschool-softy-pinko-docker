# holbertonschool-softy-pinko-docker

Docker project for building a small multi-container web stack step by step:

- `task0`: first Ubuntu-based Docker image
- `task1`: Flask back-end API
- `task2`: split back-end and front-end with Nginx
- `task3`: front-end connected to back-end with CORS
- `task4`: run both services with Docker Compose
- `task5`: add an Nginx reverse proxy
- `task6`: scale the back-end horizontally

## Repository Layout

```text
task0/
task1/
task2/
task3/
task4/
task5/
task6/
```

## Requirements

- Docker Desktop or Docker Engine
- Docker Compose support

Check locally with:

```bash
docker --version
docker compose version
```

If your machine uses the legacy command, replace `docker compose` with `docker-compose`.

## Task 0

Build:

```bash
docker build -t softy-pinko:task0 ./task0
```

Run:

```bash
docker run --rm softy-pinko:task0
```

Expected output:

```text
Hello, World!
```

## Task 1

Build:

```bash
docker build -t softy-pinko:task1 ./task1
```

Run:

```bash
docker run --rm -p 5252:5252 softy-pinko:task1
```

Test:

```bash
curl http://localhost:5252/api/hello
```

Expected response:

```text
Hello, World!
```

## Task 2

Back-end build:

```bash
docker build -t softy-pinko-back-end:task2 ./task2/back-end
```

Front-end build:

```bash
docker build -t softy-pinko-front-end:task2 ./task2/front-end
```

Front-end run:

```bash
docker run --rm -p 9000:9000 softy-pinko-front-end:task2
```

Open:

```text
http://localhost:9000
```

## Task 3

Back-end build:

```bash
docker build -t softy-pinko-back-end:task3 ./task3/back-end
```

Front-end build:

```bash
docker build -t softy-pinko-front-end:task3 ./task3/front-end
```

Run the back-end:

```bash
docker run --rm -p 5252:5252 softy-pinko-back-end:task3
```

Run the front-end in a second terminal:

```bash
docker run --rm -p 9000:9000 softy-pinko-front-end:task3
```

Open:

```text
http://localhost:9000
```

The page should show dynamic content loaded from `http://localhost:5252/api/hello`.

## Task 4

Move into the task:

```bash
cd task4
```

Build:

```bash
docker compose build
```

Run:

```bash
docker compose up
```

Open:

```text
http://localhost:9000
```

## Task 5

Move into the task:

```bash
cd task5
```

Build:

```bash
docker compose build
```

Run:

```bash
docker compose up
```

Open:

```text
http://localhost
```

In this task, the proxy is the only service mapped to a host port. The front-end and back-end stay internal to Docker.

## Task 6

Move into the task:

```bash
cd task6
```

Build:

```bash
docker compose build
```

Run with two API servers:

```bash
docker compose up --scale back-end=2
```

The same command is stored in `task6/2-api-servers.txt`.

Open:

```text
http://localhost
```

Reload the page several times and watch the back-end container logs rotate between `back-end-1` and `back-end-2`.

## Notes

- `task3`, `task4`, `task5`, and `task6` use `flask-cors` so the front-end can call the API.
- `task5` and `task6` use Nginx as a reverse proxy for `/` and `/api`.
- `task6` relies on Docker Compose scaling for round-robin balancing across multiple `back-end` containers.
