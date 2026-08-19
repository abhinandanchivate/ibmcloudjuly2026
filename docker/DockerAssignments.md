
### Assignment 1 — Container Basics

Use the `nginx` image.

Tasks:

1. Pull `nginx`.
2. List Docker images.
3. Run nginx in detached mode.
4. Name the container `my-nginx`.
5. Map host port `8080` to container port `80`.
6. Verify it is running.
7. Stop and restart it.
8. Remove the container.

Commands to explore:

```bash
docker pull
docker images
docker run
docker ps
docker stop
docker start
docker rm
```

---

### Assignment 2 — Container Investigation

Run an Ubuntu container.

Tasks:

1. Download `ubuntu`.
2. Start an interactive Ubuntu container.
3. Execute:

```bash
pwd
ls
cat /etc/os-release
```

4. Exit the container.
5. Start it again.
6. Execute a command inside it without entering interactively.
7. Inspect complete container information.

Commands:

```bash
docker run -it
docker exec
docker ps -a
docker inspect
docker start
```

---

### Assignment 3 — Docker Logs and Monitoring

Run an nginx container called:

```text
web-server
```

Tasks:

1. Run nginx on port `8081`.
2. Access it from the browser.
3. Display container logs.
4. Follow logs continuously.
5. Check running processes.
6. Check CPU and memory consumption.

Commands:

```bash
docker logs
docker logs -f
docker top
docker stats
```

---

### Assignment 4 — Docker Image Management

Work with multiple images.

Tasks:

1. Pull:

```text
nginx
redis
postgres
ubuntu
```

2. Display all images.
3. Check image history.
4. Inspect an image.
5. Remove one image.
6. Remove unused images.

Commands:

```bash
docker pull
docker images
docker history
docker image inspect
docker rmi
docker image prune
```

---

### Assignment 5 — Port Mapping

Run **three nginx containers simultaneously**.

Requirements:

| Container | Host Port | Container Port |
| --------- | --------: | -------------: |
| nginx1    |      8081 |             80 |
| nginx2    |      8082 |             80 |
| nginx3    |      8083 |             80 |

Verify using:

```text
http://localhost:8081
http://localhost:8082
http://localhost:8083
```

Commands:

```bash
docker run -d
docker ps
docker port
```

---

### Assignment 6 — Docker Volume

Create persistent storage.

Tasks:

1. Create a volume:

```text
employee-data
```

2. List volumes.
3. Inspect the volume.
4. Attach it to an Ubuntu container at:

```text
/data
```

5. Create:

```text
/data/employees.txt
```

6. Delete the container.
7. Start another container using the same volume.
8. Verify that `employees.txt` still exists.

Commands:

```bash
docker volume create
docker volume ls
docker volume inspect
docker run -v
docker exec
```

---

### Assignment 7 — Docker Network

Create communication between containers.

Tasks:

1. Create a network:

```text
employee-network
```

2. Run nginx container:

```text
frontend
```

3. Run Ubuntu container:

```text
client
```

4. Connect both to `employee-network`.
5. From the client container, try communicating with:

```text
frontend
```

6. Inspect the network.
7. Disconnect one container.
8. Remove the network.

Commands:

```bash
docker network create
docker network ls
docker network inspect
docker network connect
docker network disconnect
docker network rm
```

---

### Assignment 8 — Environment Variables

Run PostgreSQL using Docker.

Requirements:

```text
Database: employee_db
Username: admin
Password: admin123
```

Tasks:

1. Pull PostgreSQL.
2. Run it as:

```text
employee-postgres
```

3. Pass configuration using environment variables.
4. Map PostgreSQL port `5432`.
5. Verify the container.
6. Inspect environment variables.
7. Check PostgreSQL logs.

Example concepts:

```bash
docker run -d \
  --name employee-postgres \
  -e POSTGRES_DB=employee_db \
  -e POSTGRES_USER=admin \
  -e POSTGRES_PASSWORD=admin123 \
  -p 5432:5432 \
  postgres
```

---

### Assignment 9 — Build Your Own Docker Image

Create a simple HTML application.

Create:

```text
docker-assignment/
├── index.html
└── Dockerfile
```

`index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Docker Assignment</title>
</head>
<body>
    <h1>Hello Docker!</h1>
    <p>My first custom Docker image.</p>
</body>
</html>
```

Dockerfile:

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80
```

Tasks:

1. Build image:

```text
employee-web:v1
```

2. List images.
3. Run the image.
4. Map it to port `9090`.
5. Open it in browser.
6. Display image history.
7. Tag it as:

```text
employee-web:latest
```

Commands:

```bash
docker build
docker images
docker run
docker history
docker tag
```

---

### Assignment 10 — Complete Docker Challenge

Create a mini **Employee Application infrastructure**.

You need:

```text
Employee Backend
      |
      v
PostgreSQL
```

Requirements:

**PostgreSQL**

```text
Container: employee-db
Database: employee_db
Username: postgres
Password: postgres
Port: 5432
```

**Backend**

```text
Container: employee-api
Port: 8080
```

**Network**

```text
employee-network
```

**Volume**

```text
employee-db-data
```

Tasks:

1. Create the network.
2. Create the volume.
3. Start PostgreSQL.
4. Attach PostgreSQL to the volume.
5. Attach PostgreSQL to the custom network.
6. Start the Employee API.
7. Connect it to PostgreSQL using container name `employee-db`.
8. Check both containers.
9. View backend logs.
10. View database logs.
11. Inspect the network.
12. Inspect the volume.
13. Check resource utilization.
14. Stop everything.
15. Delete containers.
16. Remove unused resources.

Important commands:

```bash
docker pull
docker build
docker run
docker ps
docker ps -a
docker images
docker exec
docker logs
docker inspect
docker stats
docker stop
docker start
docker restart
docker rm
docker rmi
docker volume create
docker volume ls
docker volume inspect
docker network create
docker network ls
docker network inspect
docker system df
docker system prune
```

### Bonus Challenge

Without referring to notes, explain what these commands do:

```bash
docker run -d
docker run -it
docker exec -it
docker ps
docker ps -a
docker logs -f
docker inspect
docker rm -f
docker rmi
docker image prune
docker container prune
docker volume prune
docker network prune
docker system prune
```
