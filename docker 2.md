
---

# 🐳Docker Compose Commands (Interview + Industry Ready)

## 🎯 Think of Docker Compose like this

Suppose your project contains:

```
Employee Management
│
├── Spring Boot
├── MySQL
├── Redis
└── Kafka
```

Instead of managing each container individually, Docker Compose manages **the whole application**.

---

# 1️⃣ docker compose up ⭐⭐⭐⭐⭐

## What does it do?

Creates and starts all containers defined in `docker-compose.yml`.

```bash
docker compose up
```

### Flow

```
Read docker-compose.yml
        │
        ▼
Create Network
        │
        ▼
Create Volume
        │
        ▼
Start MySQL
        │
        ▼
Start Spring Boot
```

---

## When do we use it?

* First time starting the project
* Starting all services together

---

# 2️⃣ docker compose up -d ⭐⭐⭐⭐⭐

Most commonly used command.

```bash
docker compose up -d
```

`-d` means **Detached Mode**.

Without `-d`

```
Terminal
│
Application Logs
│
██████████
```

You can't use that terminal.

With `-d`

```
Application runs in background ✅

Terminal becomes free ✅
```

---

# 3️⃣ docker compose up --build ⭐⭐⭐⭐⭐

Suppose you changed Java code.

```
Controller

↓

Service

↓

Entity
```

Need to rebuild the image.

Run:

```bash
docker compose up --build
```

It automatically:

```
Build New Image

↓

Remove Old Container

↓

Start New Container
```

Equivalent to:

```bash
mvn clean package
docker build
docker run
```

---

# 4️⃣ docker compose down ⭐⭐⭐⭐⭐

Stops and removes all containers.

```bash
docker compose down
```

Flow

```
Stop Spring Boot

↓

Stop MySQL

↓

Remove Containers

↓

Network Removed
```

---

### Does it remove the database?

If using a **Volume**

```
NO ✅
```

If not using a volume

```
Data Lost ❌
```

---

# 5️⃣ docker compose stop

Only stops containers.

```bash
docker compose stop
```

```
Container Exists

↓

Only Stopped
```

---

# 6️⃣ docker compose start

Starts stopped containers.

```bash
docker compose start
```

No rebuilding.

No recreation.

---

# 7️⃣ docker compose restart

Restart all services.

```bash
docker compose restart
```

Useful after:

* Environment changes
* Configuration changes
* Temporary issues

---

# 8️⃣ docker compose ps

Shows running services.

```bash
docker compose ps
```

Example

```
NAME                 STATUS

employee-container   Up

mysql-db             Up
```

---

# 9️⃣ docker compose logs ⭐⭐⭐⭐⭐

View logs.

```bash
docker compose logs
```

For one service

```bash
docker compose logs employee-app
```

Follow live logs

```bash
docker compose logs -f
```

Exactly like

```bash
docker logs -f employee-container
```

---

# 🔟 docker compose exec ⭐⭐⭐⭐⭐

Execute commands inside a running container.

Example

```bash
docker compose exec mysql bash
```

Now you're inside MySQL container.

Or

```bash
docker compose exec employee-app sh
```

Inside Spring Boot container.

Very useful for debugging.

---

# 1️⃣1️⃣ docker compose pull

Downloads latest images.

```bash
docker compose pull
```

Useful when

```
MySQL 8.0

↓

Latest Patch Released

↓

Pull Latest Image
```

---

# 1️⃣2️⃣ docker compose build

Only builds images.

```bash
docker compose build
```

No container started.

---

# Real Developer Workflow

## Morning

Start project

```bash
docker compose up -d
```

---

### Changed Java Code

```bash
mvn clean package -DskipTests
```

↓

```bash
docker compose up --build -d
```

---

### Check Logs

```bash
docker compose logs -f
```

---

### Going Home

```bash
docker compose down
```

---

# Interview Cheat Sheet

| Command                     | Purpose                           |
| --------------------------- | --------------------------------- |
| `docker compose up`         | Create and start all services     |
| `docker compose up -d`      | Start in background               |
| `docker compose up --build` | Rebuild image and start           |
| `docker compose down`       | Stop and remove containers        |
| `docker compose stop`       | Stop containers only              |
| `docker compose start`      | Start stopped containers          |
| `docker compose restart`    | Restart containers                |
| `docker compose ps`         | Show running services             |
| `docker compose logs`       | View logs                         |
| `docker compose logs -f`    | Follow live logs                  |
| `docker compose exec`       | Execute commands inside container |
| `docker compose build`      | Build images only                 |
| `docker compose pull`       | Download latest images            |

---

# 🎤 Interview Script (Directly Speak)

**Q. Explain your Docker workflow in your Spring Boot project.**

> "Our project uses Docker Compose to manage multiple services like Spring Boot and MySQL. We define them in a `docker-compose.yml` file. During development, after code changes, I package the application using Maven and run `docker compose up --build -d` to rebuild the image and start the updated containers. I use `docker compose logs -f` for debugging and `docker compose down` when I want to stop and clean up the environment."

---
