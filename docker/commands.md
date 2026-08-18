# Docker Commands – 
---

# 1. `docker --version`

```bash
docker --version
```

Example:

```bash
Docker version 28.x.x
```

### 5W1H

| Question   | Explanation                                          |
| ---------- | ---------------------------------------------------- |
| **What?**  | Displays the installed Docker version.               |
| **Why?**   | To verify Docker is installed correctly.             |
| **When?**  | Before starting Docker-based development.            |
| **Where?** | Terminal / Command Prompt / PowerShell.              |
| **Who?**   | Developers, DevOps engineers, system administrators. |
| **How?**   | Execute `docker --version`.                          |

---

# 2. `docker info`

```bash
docker info
```

### What?

Shows detailed Docker environment information.

It displays information such as:

```text
Containers
Images
Docker Engine Version
Storage Driver
CPUs
Memory
Docker Root Directory
```

### Why?

Useful for checking whether Docker Engine is running correctly.

### Example

```bash
docker info
```

---

# 3. `docker pull`

Syntax:

```bash
docker pull <image-name>
```

Example:

```bash
docker pull nginx
```

Another example:

```bash
docker pull mysql:8
```

### 5W1H

| Question   | Explanation                                             |
| ---------- | ------------------------------------------------------- |
| **What?**  | Downloads a Docker image.                               |
| **Why?**   | We need an image before creating a container.           |
| **When?**  | When the required image is not available locally.       |
| **Where?** | Usually downloaded from Docker Hub or another registry. |
| **Who?**   | Developers and DevOps engineers.                        |
| **How?**   | `docker pull nginx`                                     |

### Flow

```text
Docker Hub
    ↓
docker pull nginx
    ↓
Docker Image
    ↓
Stored Locally
```

---

# 4. `docker images`

```bash
docker images
```

or:

```bash
docker image ls
```

Example output:

```text
REPOSITORY   TAG       IMAGE ID       SIZE
nginx        latest    123abc456      190MB
mysql        8         456def789      600MB
```

### What?

Displays locally available Docker images.

### Why?

To check which images have already been downloaded or created.

---

# 5. `docker run`

One of the most important Docker commands.

Syntax:

```bash
docker run <image>
```

Example:

```bash
docker run nginx
```

### 5W1H

| Question   | Explanation                                                  |
| ---------- | ------------------------------------------------------------ |
| **What?**  | Creates and starts a container from an image.                |
| **Why?**   | To actually execute an application packaged inside an image. |
| **When?**  | When you want to start a new container.                      |
| **Where?** | Docker Engine executes the container.                        |
| **Who?**   | Developers, testers and DevOps engineers.                    |
| **How?**   | `docker run nginx`                                           |

### Important concept

```text
Image
  ↓
docker run
  ↓
Container
```

Think:

```text
Class → Object
Image → Container
```

An **image is a blueprint**, while a **container is a running instance of that image**.

---

# 6. Run Container in Background

```bash
docker run -d nginx
```

`-d` means:

```text
Detached Mode
```

Without `-d`:

```bash
docker run nginx
```

the terminal remains attached to the container.

With:

```bash
docker run -d nginx
```

the container executes in the background.

---

# 7. `docker ps`

```bash
docker ps
```

### What?

Displays running containers.

Example:

```text
CONTAINER ID   IMAGE   STATUS       PORTS
a12bc34        nginx   Up 2 mins    80/tcp
```

### Why?

To see which Docker containers are currently running.

---

# 8. Display All Containers

```bash
docker ps -a
```

`-a` means:

```text
all
```

It displays:

```text
Running Containers
Stopped Containers
Exited Containers
Created Containers
```

Example:

```bash
docker ps -a
```

---

# 9. Container Naming

Instead of Docker generating a random name:

```bash
docker run -d --name my-nginx nginx
```

Check:

```bash
docker ps
```

Example:

```text
CONTAINER ID   IMAGE   NAME
abc123         nginx   my-nginx
```

### Why name containers?

Instead of:

```bash
docker stop abc123
```

you can write:

```bash
docker stop my-nginx
```

Much easier.

---

# 10. Port Mapping

One of the most important Docker concepts.

```bash
docker run -d -p 8080:80 nginx
```

Format:

```text
-p HOST_PORT:CONTAINER_PORT
```

Here:

```text
8080 → Host/Mac/Windows
80   → Nginx inside container
```

Then open:

```text
http://localhost:8080
```

### 5W1H

| Question   | Explanation                                             |
| ---------- | ------------------------------------------------------- |
| **What?**  | Connects host port with container port.                 |
| **Why?**   | Containers have isolated networking.                    |
| **When?**  | When the application must be accessible outside Docker. |
| **Where?** | Between host machine and Docker container.              |
| **Who?**   | Developers configuring application networking.          |
| **How?**   | `docker run -p 8080:80 nginx`                           |

Diagram:

```text
Browser
   ↓
localhost:8080
   ↓
Host Port 8080
   ↓
Docker
   ↓
Container Port 80
   ↓
Nginx
```

---

# 11. `docker stop`

```bash
docker stop <container>
```

Example:

```bash
docker stop my-nginx
```

### What?

Gracefully stops a running container.

---

# 12. `docker start`

```bash
docker start my-nginx
```

### What?

Starts an already-created stopped container.

Important difference:

```text
docker run
    ↓
Creates + Starts

docker start
    ↓
Starts existing container
```

---

# 13. `docker restart`

```bash
docker restart my-nginx
```

Equivalent conceptually to:

```text
docker stop
+
docker start
```

Example:

```bash
docker restart my-nginx
```

---

# 14. `docker rm`

Remove a container:

```bash
docker rm my-nginx
```

The container normally needs to be stopped first:

```bash
docker stop my-nginx
docker rm my-nginx
```

Force remove:

```bash
docker rm -f my-nginx
```

---

# 15. `docker rmi`

Remove an image:

```bash
docker rmi nginx
```

or:

```bash
docker image rm nginx
```

### Important difference

```text
docker rm
   ↓
Remove Container

docker rmi
   ↓
Remove Image
```

---

# 16. `docker logs`

Syntax:

```bash
docker logs <container-name>
```

Example:

```bash
docker logs my-nginx
```

### What?

Displays application/container logs.

### Why?

Useful for debugging.

Example for Spring Boot:

```bash
docker logs employee-service
```

Possible output:

```text
Started EmployeeApplication
Tomcat started on port 8080
Connected to database
```

Follow logs continuously:

```bash
docker logs -f employee-service
```

`-f` means:

```text
follow
```

Similar to:

```bash
tail -f
```

---

# 17. Execute Command Inside Container

```bash
docker exec
```

Example:

```bash
docker exec my-nginx ls
```

Run interactive shell:

```bash
docker exec -it my-nginx /bin/bash
```

Sometimes lightweight images use:

```bash
docker exec -it my-nginx /bin/sh
```

### 5W1H

| Question   | Explanation                                      |
| ---------- | ------------------------------------------------ |
| **What?**  | Executes a command inside an existing container. |
| **Why?**   | Debugging or inspecting the container.           |
| **When?**  | When the container is already running.           |
| **Where?** | Inside the container environment.                |
| **Who?**   | Developers / DevOps engineers.                   |
| **How?**   | `docker exec -it container bash`                 |

---

# 18. Inspect Container

```bash
docker inspect my-nginx
```

Displays detailed information such as:

```text
Container ID
IP Address
Environment Variables
Volumes
Networks
Ports
Configuration
```

Useful command:

```bash
docker inspect my-nginx
```

---

# 19. Environment Variables

Example with MySQL:

```bash
docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=root123 \
  -e MYSQL_DATABASE=employee_db \
  mysql:8
```

`-e` means:

```text
Environment Variable
```

Inside the MySQL container:

```text
MYSQL_ROOT_PASSWORD=root123
MYSQL_DATABASE=employee_db
```

---

# 20. Volume

Containers are temporary.

Suppose MySQL stores data inside:

```text
/var/lib/mysql
```

If we remove the container, the data may disappear.

Therefore, use a **volume**.

Create volume:

```bash
docker volume create mysql-data
```

Check volumes:

```bash
docker volume ls
```

Run MySQL:

```bash
docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=root123 \
  -v mysql-data:/var/lib/mysql \
  mysql:8
```

### 5W1H of Docker Volume

| Question   | Explanation                                                  |
| ---------- | ------------------------------------------------------------ |
| **What?**  | Persistent Docker storage.                                   |
| **Why?**   | Container data shouldn't disappear after container deletion. |
| **When?**  | Databases, uploaded files, persistent application data.      |
| **Where?** | Managed by Docker on the host machine.                       |
| **Who?**   | Applications requiring persistent storage.                   |
| **How?**   | `-v volume-name:/container/path`                             |

Architecture:

```text
Container
   ↓
/var/lib/mysql
   ↓
Docker Volume
   ↓
mysql-data
   ↓
Persistent Data
```

---

# 21. Bind Mount

Another storage option:

```bash
docker run -d \
  -v $(pwd):/app \
  my-app
```

Meaning:

```text
Current Host Directory
        ↓
       /app
        ↓
Docker Container
```

Commonly used during development.

---

# 22. Docker Network

Create network:

```bash
docker network create app-network
```

View networks:

```bash
docker network ls
```

Run database:

```bash
docker run -d \
  --name mysql-db \
  --network app-network \
  -e MYSQL_ROOT_PASSWORD=root \
  mysql:8
```

Run application:

```bash
docker run -d \
  --name employee-service \
  --network app-network \
  employee-service
```

Now the application can communicate with MySQL using:

```text
mysql-db
```

instead of:

```text
localhost
```

---

# 23. Why `localhost` Doesn't Work Between Containers

Consider:

```text
Employee Container
MySQL Container
```

Inside `Employee Container`:

```text
localhost
```

means:

```text
Employee Container itself
```

It does **not** mean MySQL.

Therefore:

```text
jdbc:mysql://localhost:3306/db
```

is wrong.

Use:

```text
jdbc:mysql://mysql-db:3306/db
```

where:

```text
mysql-db = Docker container/service name
```

---

# 24. Build Docker Image

If you have:

```text
Dockerfile
```

Run:

```bash
docker build -t employee-service .
```

### Explanation

```text
docker build
     ↓
Read Dockerfile
     ↓
Create Layers
     ↓
Create Docker Image
```

`-t` means:

```text
tag/name
```

`.` means:

```text
Use current directory as build context
```

---

# 25. Dockerfile Example – Spring Boot

```dockerfile
FROM eclipse-temurin:21-jre

WORKDIR /app

COPY target/employee-service.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
```

### 5W1H

### What?

Dockerfile defines how a Docker image should be created.

### Why?

So application packaging becomes repeatable.

### When?

When creating a custom application image.

### Where?

Normally in the project root directory.

Example:

```text
employee-service/
│
├── src/
├── pom.xml
├── Dockerfile
└── target/
    └── employee-service.jar
```

### Who?

Developer / DevOps engineer.

### How?

```bash
docker build -t employee-service .
```

---

# 26. Run Spring Boot Image

After building:

```bash
docker run -d \
  --name employee-service \
  -p 8080:8080 \
  employee-service
```

Test:

```text
http://localhost:8080
```

---

# 27. Docker Tag

```bash
docker tag employee-service abhi/employee-service:v1
```

Concept:

```text
employee-service
       ↓
tag
       ↓
abhi/employee-service:v1
```

Useful before pushing an image to a registry.

---

# 28. `docker login`

```bash
docker login
```

Used to authenticate with Docker Hub/container registry.

---

# 29. `docker push`

```bash
docker push abhi/employee-service:v1
```

Flow:

```text
Dockerfile
   ↓
docker build
   ↓
Image
   ↓
docker tag
   ↓
docker login
   ↓
docker push
   ↓
Docker Registry
```

---

# 30. Docker Compose

Instead of manually running:

```bash
docker run mysql...
docker run employee...
docker run department...
docker run gateway...
```

we can define everything in:

```text
compose.yaml
```

Example:

```yaml
services:

  mysql:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: employee_db

  employee-service:
    build: ./employee-service
    ports:
      - "8081:8080"
    depends_on:
      - mysql
```

Run everything:

```bash
docker compose up
```

Run in background:

```bash
docker compose up -d
```

---

# 31. Docker Compose 5W1H

| Question   | Explanation                                          |
| ---------- | ---------------------------------------------------- |
| **What?**  | Tool for running multiple related containers.        |
| **Why?**   | Avoid executing many `docker run` commands manually. |
| **When?**  | Microservices and multi-container applications.      |
| **Where?** | Configuration is normally stored in `compose.yaml`.  |
| **Who?**   | Developers / DevOps / deployment teams.              |
| **How?**   | `docker compose up -d`                               |

---

# 32. Docker Compose Commands

Start:

```bash
docker compose up
```

Background:

```bash
docker compose up -d
```

Stop:

```bash
docker compose stop
```

Start again:

```bash
docker compose start
```

Restart:

```bash
docker compose restart
```

Remove containers:

```bash
docker compose down
```

Remove containers + volumes:

```bash
docker compose down -v
```

Check:

```bash
docker compose ps
```

Logs:

```bash
docker compose logs
```

Follow logs:

```bash
docker compose logs -f
```

Build:

```bash
docker compose build
```

Rebuild and run:

```bash
docker compose up -d --build
```

---

# 33. Docker Cleanup Commands

Stopped containers:

```bash
docker container prune
```

Unused images:

```bash
docker image prune
```

Unused volumes:

```bash
docker volume prune
```

Unused networks:

```bash
docker network prune
```

Clean unused Docker resources:

```bash
docker system prune
```

More aggressive:

```bash
docker system prune -a
```

Use the `-a` option carefully because it removes unused images too.

---

# 34. Complete Nginx Practical Example

### Step 1 — Download image

```bash
docker pull nginx
```

### Step 2 — Check image

```bash
docker images
```

### Step 3 — Create container

```bash
docker run -d \
  --name nginx-server \
  -p 8080:80 \
  nginx
```

### Step 4 — Check container

```bash
docker ps
```

### Step 5 — Open browser

```text
http://localhost:8080
```

### Step 6 — Check logs

```bash
docker logs nginx-server
```

### Step 7 — Stop

```bash
docker stop nginx-server
```

### Step 8 — Start

```bash
docker start nginx-server
```

### Step 9 — Remove

```bash
docker stop nginx-server
docker rm nginx-server
```

### Step 10 — Remove image

```bash
docker rmi nginx
```

---

# 35. Complete MySQL Practical Example

```bash
docker run -d \
  --name mysql-db \
  -p 3306:3306 \
  -e MYSQL_ROOT_PASSWORD=root123 \
  -e MYSQL_DATABASE=company_db \
  -e MYSQL_USER=admin \
  -e MYSQL_PASSWORD=admin123 \
  -v mysql-data:/var/lib/mysql \
  mysql:8
```

Check:

```bash
docker ps
```

Logs:

```bash
docker logs mysql-db
```

Connect to MySQL:

```bash
docker exec -it mysql-db mysql -u root -p
```

Enter:

```text
root123
```

Then:

```sql
SHOW DATABASES;
```

---

# 36. Important Docker Command Cheat Sheet

| Requirement         | Command                         |
| ------------------- | ------------------------------- |
| Check Docker        | `docker --version`              |
| Docker details      | `docker info`                   |
| Download image      | `docker pull nginx`             |
| List images         | `docker images`                 |
| Run container       | `docker run nginx`              |
| Background run      | `docker run -d nginx`           |
| Name container      | `docker run --name app nginx`   |
| Port mapping        | `docker run -p 8080:80 nginx`   |
| Running containers  | `docker ps`                     |
| All containers      | `docker ps -a`                  |
| Stop                | `docker stop app`               |
| Start               | `docker start app`              |
| Restart             | `docker restart app`            |
| Logs                | `docker logs app`               |
| Follow logs         | `docker logs -f app`            |
| Enter container     | `docker exec -it app /bin/bash` |
| Inspect             | `docker inspect app`            |
| Delete container    | `docker rm app`                 |
| Delete image        | `docker rmi nginx`              |
| Create volume       | `docker volume create data`     |
| List volumes        | `docker volume ls`              |
| Create network      | `docker network create app-net` |
| List networks       | `docker network ls`             |
| Build image         | `docker build -t app .`         |
| Compose start       | `docker compose up -d`          |
| Compose stop/remove | `docker compose down`           |
| Compose rebuild     | `docker compose up -d --build`  |

---

## Most important Docker flow for students

```text
Dockerfile
   ↓
docker build
   ↓
Docker Image
   ↓
docker run
   ↓
Docker Container
   ↓
Application Running
```

And for a microservices project:

```text
Spring Boot Service
       ↓
    Dockerfile
       ↓
  docker build
       ↓
 Docker Image
       ↓
 compose.yaml
       ↓
docker compose up -d
       ↓
┌─────────────────────┐
│ API Gateway         │
│ Employee Service    │
│ Department Service  │
│ Eureka Server       │
│ Config Server       │
│ MySQL/PostgreSQL    │
└─────────────────────┘
```
