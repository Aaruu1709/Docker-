
# 🐳 Module 3 – Real Industry Docker Compose Project

---

# 🏗️ Project Structure

```text
EmployeeManagement/
│
├── src/
├── target/
├── Dockerfile
├── docker-compose.yml ⭐
├── pom.xml
├── README.md
└── .dockerignore ⭐
```

Notice one new file:

```text
.dockerignore
```

We'll understand why we need it.

---

# Before Understanding Compose

Let's understand how the application starts.

```text
Developer

↓

docker compose up --build

↓

Read docker-compose.yml

↓

Build Spring Boot Image

↓

Pull MySQL Image

↓

Create Network

↓

Create Volume

↓

Start MySQL

↓

Wait

↓

Start Spring Boot

↓

Application Ready
```

---

# Industry docker-compose.yml

```yaml
services:

  mysql:

    image: mysql:8.0

    container_name: mysql-db

    restart: always

    environment:

      MYSQL_ROOT_PASSWORD: root

      MYSQL_DATABASE: employeemanagement

    ports:

      - "3306:3306"

    volumes:

      - mysql-data:/var/lib/mysql

    healthcheck:

      test: ["CMD","mysqladmin","ping","-h","localhost"]

      interval: 10s

      retries: 5

      timeout: 5s

    networks:

      - employee-network

  employee-app:

    build: .

    container_name: employee-container

    restart: always

    ports:

      - "8081:8081"

    environment:

      SPRING_PROFILES_ACTIVE: docker

    depends_on:

      mysql:

        condition: service_healthy

    networks:

      - employee-network

volumes:

  mysql-data:

networks:

  employee-network:
```

This looks large.

Don't worry.

Let's understand line by line.

---

# ⭐ restart: always

```yaml
restart: always
```

Meaning

```text
Application Crashed

↓

Docker detects failure

↓

Automatically Restart
```

Without this

```text
Application Crash

↓

Stopped Forever
```

Real companies almost always use a restart policy.

---

# ⭐ Health Check

This is one of the favorite interview questions.

```yaml
healthcheck:
```

means

> "Is my database actually ready?"

Not

```text
Container Running
```

Running doesn't always mean ready.

Example

```text
MySQL Container Started

↓

Still Loading Database

↓

Spring Boot Connects

↓

Connection Failed
```

Health check waits until

```text
MySQL says

"I'm Ready"

↓

Now Start Spring Boot
```

---

# ⭐ condition: service_healthy

Instead of

```yaml
depends_on:
   - mysql
```

we use

```yaml
depends_on:

  mysql:

    condition: service_healthy
```

Difference:

Old

```text
Start MySQL

↓

Immediately Start Spring Boot
```

New

```text
Start MySQL

↓

Wait Until Healthy

↓

Start Spring Boot
```

Much safer.

---

# ⭐ Named Volume

```yaml
mysql-data:
```

Think of it as

```text
Database Hard Disk
```

Even if MySQL container dies

```text
Employee Data

Salary

Users

Still Safe
```

---

# ⭐ Network

```yaml
employee-network
```

Both containers communicate like

```text
employee-app

↓

mysql
```

Never use

```text
localhost
```

inside Docker.

---

# ⭐ .dockerignore

Almost every beginner forgets this.

Create

```text
.dockerignore
```

Inside write

```text
.git

.idea

.vscode

README.md

target/*.original
```

---

## Why?

Suppose your project looks like

```text
Project

↓

10 GB

↓

Only 100 MB Needed
```

Docker copies everything unless ignored.

`.dockerignore` makes image building:

* Faster
* Smaller
* Cleaner

Exactly like `.gitignore`.

---

# Industry Folder Structure

```text
EmployeeManagement

│

├── src

├── Dockerfile

├── docker-compose.yml

├── .dockerignore

├── pom.xml

├── README.md

└── target
```

You'll see this structure in most Spring Boot repositories.

---

# Real Company Workflow

Morning

```bash
docker compose up -d
```

Changed Code

```bash
mvn clean package -DskipTests
```

↓

```bash
docker compose up --build -d
```

Debug

```bash
docker compose logs -f
```

Go Home

```bash
docker compose down
```

This is the daily workflow of many backend developers.

---

# Interview Questions

## Q1. What is a health check?

**Answer**

A health check verifies that a service is not only running but also ready to serve requests. In Docker Compose, it can be combined with `depends_on` so dependent services start only after the required service becomes healthy.

---

## Q2. Why do we use `restart: always`?

**Answer**

It automatically restarts a container if it crashes or if Docker restarts, improving application availability.

---

## Q3. What is `.dockerignore`?

**Answer**

`.dockerignore` excludes unnecessary files and folders from the Docker build context. This reduces image size and speeds up image creation.

---

# 🎤 4+ Years Experience Interview Script

> "In our Spring Boot project, we containerized the application using Docker and orchestrated services with Docker Compose. The Compose file defines Spring Boot and MySQL services, environment variables, persistent volumes for database storage, and a dedicated bridge network. We use health checks so the application starts only after MySQL is ready, and `restart: always` to improve reliability. During development, we package the application with Maven and run `docker compose up --build -d` to deploy updated containers."

---

