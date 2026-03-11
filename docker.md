# Docker & Docker Compose Basic Commands Guide

## Install Docker (Ubuntu)

```
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker
```

Check Docker version

```
docker --version
```

Add your user to the docker group (optional, to avoid sudo)

```
sudo usermod -aG docker $USER
newgrp docker
```

---

# Install Docker Compose

## Method 1: Install Docker Compose Plugin (Recommended)

```
sudo apt update
sudo apt install docker-compose-plugin
```

Check version

```
docker compose version
```

---

## Method 2: Install Standalone Docker Compose

```
sudo apt install docker-compose
```

Check version

```
docker-compose --version
```

---

# Basic Docker Commands

## Check running containers

```
docker ps
```

## Check all containers (including stopped)

```
docker ps -a
```

## List docker images

```
docker images
```

## Pull an image

```
docker pull <image_name>
```

Example

```
docker pull nginx
```

## Remove a container

```
docker rm <container_id>
```

## Remove an image

```
docker rmi <image_id>
```

## View container logs

```
docker logs <container_name>
```

Follow logs in real time

```
docker logs -f <container_name>
```

## Enter a running container

```
docker exec -it <container_name> bash
```

If bash is not available

```
docker exec -it <container_name> sh
```

---

# Basic Docker Compose Commands

Navigate to the directory containing `docker-compose.yml` before running these commands.

## Turn up containers

```
docker-compose up -d
```

## Start containers

```
docker-compose start
```

## Stop containers

```
docker-compose stop
```

## Restart containers

```
docker-compose restart
```

## View running compose containers

```
docker-compose ps
```

## View logs

```
docker-compose logs
```

Follow logs live

```
docker-compose logs -f
```

## Rebuild containers

```
docker-compose up -d --build
```

## Stop and remove containers

```
docker-compose down
```

## Stop containers and delete volumes (Reset)

⚠️ This will delete persistent data stored in volumes.

```
docker-compose down -v
```

---

# Docker Volume Commands

## List volumes

```
docker volume ls
```

## Inspect a volume

```
docker volume inspect <volume_name>
```

## Delete a volume

```
docker volume rm <volume_name>
```

---

# Docker Network Commands

## List networks

```
docker network ls
```

## Inspect network

```
docker network inspect <network_name>
```

---

# Docker Cleanup Commands

## Check Docker disk usage

```
docker system df
```

## Remove stopped containers

```
docker container prune
```

## Remove unused images

```
docker image prune
```

## Remove unused volumes

```
docker volume prune
```

## Remove unused networks

```
docker network prune
```

## Remove everything unused

```
docker system prune
```

Remove everything including volumes

```
docker system prune -a --volumes
```

---

# Quick Troubleshooting Workflow

If containers behave incorrectly:

### 1. Check logs

```
docker-compose logs -f
```

### 2. Restart containers

```
docker-compose restart
```

### 3. Rebuild containers

```
docker-compose up -d --build
```

### 4. Full reset

```
docker-compose down -v
docker-compose up -d
```

---

# Notes

- Always run commands in the directory containing `docker-compose.yml`
- Use `docker-compose logs -f` to debug most problems
- Avoid `docker-compose down -v` unless you want to wipe all container data
- Use `docker system prune` to free disk space if Docker fills your VM
