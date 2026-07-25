# Docker Commands Cheat Sheet: Every Command You'll Actually Use

*By Nilavanan S A*

Whether you're building images, managing containers, or cleaning up disk space, this guide covers the essential Docker CLI commands with real-world usage examples — organized so you can quickly find what you need.

---

## Table of Contents

1. [Docker Info & Setup](#1-docker-info--setup)
2. [Image Commands](#2-image-commands)
3. [Container Commands](#3-container-commands)
4. [Container Lifecycle](#4-container-lifecycle)
5. [Executing & Inspecting Containers](#5-executing--inspecting-containers)
6. [Volume Commands](#6-volume-commands)
7. [Network Commands](#7-network-commands)
8. [Docker Compose Commands](#8-docker-compose-commands)
9. [Docker Swarm Commands](#9-docker-swarm-commands)
10. [System & Cleanup Commands](#10-system--cleanup-commands)
11. [Registry & Login Commands](#11-registry--login-commands)
12. [Handy Flags Reference](#12-handy-flags-reference)

---

## 1. Docker Info & Setup

```bash
# Check Docker version
docker --version

# Show detailed version info (client + server)
docker version

# Display system-wide information (containers, images, storage driver, etc.)
docker info

# Show help for any command
docker <command> --help
```

---

## 2. Image Commands

```bash
# Build an image from a Dockerfile in the current directory
docker build -t myapp:1.0 .

# Build using a specific Dockerfile
docker build -t myapp:1.0 -f Dockerfile.prod .

# Build without using cache
docker build --no-cache -t myapp:1.0 .

# List all local images
docker images
docker image ls

# Pull an image from Docker Hub
docker pull nginx:latest

# Push an image to a registry
docker push myrepo/myapp:1.0

# Tag an image
docker tag myapp:1.0 myrepo/myapp:1.0

# Remove an image
docker rmi myapp:1.0

# Remove all unused (dangling) images
docker image prune

# Remove ALL unused images, not just dangling ones
docker image prune -a

# Inspect image metadata (layers, env vars, config)
docker inspect myapp:1.0

# View the build history/layers of an image
docker history myapp:1.0

# Save an image to a tar file
docker save -o myapp.tar myapp:1.0

# Load an image from a tar file
docker load -i myapp.tar

# Search Docker Hub for an image
docker search nginx
```

---

## 3. Container Commands

```bash
# Run a container (foreground)
docker run myapp:1.0

# Run in detached (background) mode
docker run -d myapp:1.0

# Run with a custom name
docker run -d --name my-container myapp:1.0

# Run with port mapping (host:container)
docker run -d -p 8080:80 myapp:1.0

# Run with an environment variable
docker run -d -e NODE_ENV=production myapp:1.0

# Run with a volume mounted
docker run -d -v myvolume:/app/data myapp:1.0

# Run with a bind mount (host path to container path)
docker run -d -v /host/path:/container/path myapp:1.0

# Run and remove container automatically on exit
docker run --rm myapp:1.0

# Run interactively with a terminal (useful for debugging)
docker run -it myapp:1.0 /bin/bash

# Limit CPU and memory usage
docker run -d --cpus="1.5" --memory="512m" myapp:1.0

# Set a restart policy
docker run -d --restart unless-stopped myapp:1.0
```

---

## 4. Container Lifecycle

```bash
# List running containers
docker ps

# List all containers, including stopped ones
docker ps -a

# Start a stopped container
docker start <container_id_or_name>

# Stop a running container (graceful, SIGTERM)
docker stop <container_id_or_name>

# Force kill a container (SIGKILL)
docker kill <container_id_or_name>

# Restart a container
docker restart <container_id_or_name>

# Pause a container (freezes all processes)
docker pause <container_id_or_name>

# Unpause a container
docker unpause <container_id_or_name>

# Remove a stopped container
docker rm <container_id_or_name>

# Force remove a running container
docker rm -f <container_id_or_name>

# Remove all stopped containers
docker container prune

# Rename a container
docker rename old_name new_name
```

---

## 5. Executing & Inspecting Containers

```bash
# Open an interactive shell in a running container
docker exec -it <container_id_or_name> /bin/bash

# Run a one-off command inside a running container
docker exec <container_id_or_name> ls /app

# View container logs
docker logs <container_id_or_name>

# Follow logs in real time (like tail -f)
docker logs -f <container_id_or_name>

# Show last N lines of logs
docker logs --tail 100 <container_id_or_name>

# Inspect full container metadata (JSON)
docker inspect <container_id_or_name>

# View real-time resource usage (CPU, memory, network)
docker stats

# View resource usage for a specific container
docker stats <container_id_or_name>

# List running processes inside a container
docker top <container_id_or_name>

# Copy files from host to container
docker cp ./file.txt <container_id_or_name>:/app/file.txt

# Copy files from container to host
docker cp <container_id_or_name>:/app/file.txt ./file.txt

# Show port mappings for a container
docker port <container_id_or_name>

# Show changes made to a container's filesystem since it started
docker diff <container_id_or_name>
```

---

## 6. Volume Commands

```bash
# Create a named volume
docker volume create myvolume

# List all volumes
docker volume ls

# Inspect a volume's details
docker volume inspect myvolume

# Remove a specific volume
docker volume rm myvolume

# Remove all unused volumes
docker volume prune
```

---

## 7. Network Commands

```bash
# List all networks
docker network ls

# Create a custom bridge network
docker network create mynetwork

# Create a network with a specific driver
docker network create --driver overlay mynetwork

# Inspect a network (see connected containers, subnet, etc.)
docker network inspect mynetwork

# Connect a running container to a network
docker network connect mynetwork <container_id_or_name>

# Disconnect a container from a network
docker network disconnect mynetwork <container_id_or_name>

# Remove a network
docker network rm mynetwork

# Remove all unused networks
docker network prune
```

---

## 8. Docker Compose Commands

```bash
# Start all services defined in docker-compose.yml
docker compose up

# Start in detached mode
docker compose up -d

# Rebuild images before starting
docker compose up --build

# Stop and remove containers, networks (keeps volumes)
docker compose down

# Stop and remove containers, networks, AND volumes
docker compose down -v

# List running compose services
docker compose ps

# View logs for all services
docker compose logs -f

# Scale a specific service to N instances
docker compose up --scale worker=3

# Execute a command in a running service container
docker compose exec web /bin/bash

# Validate and view the resolved compose configuration
docker compose config

# Restart a specific service
docker compose restart web
```

---

## 9. Docker Swarm Commands

```bash
# Initialize a new swarm
docker swarm init

# Get the join token for a worker node
docker swarm join-token worker

# Join a swarm as a worker
docker swarm join --token <token> <manager_ip>:2377

# List nodes in the swarm
docker node ls

# Deploy a stack from a compose file
docker stack deploy -c docker-compose.yml mystack

# List running stacks
docker stack ls

# List services in a stack
docker stack services mystack

# Remove a stack
docker stack rm mystack

# Create a service
docker service create --name web --replicas 3 -p 80:80 nginx

# Scale a service
docker service scale web=5

# Update a service (e.g., new image version)
docker service update --image myapp:2.0 web

# Leave the swarm
docker swarm leave --force
```

---

## 10. System & Cleanup Commands

```bash
# Show disk usage by Docker (images, containers, volumes, cache)
docker system df

# Remove all unused containers, networks, and dangling images
docker system prune

# Remove everything unused, including unused images and volumes
docker system prune -a --volumes

# Remove all stopped containers
docker container prune

# Remove all unused images (not just dangling ones)
docker image prune -a

# Remove build cache
docker builder prune
```

---

## 11. Registry & Login Commands

```bash
# Log in to Docker Hub (or another registry)
docker login

# Log in to a private registry
docker login myregistry.example.com

# Log out
docker logout

# Push an image to a registry
docker push myrepo/myapp:1.0

# Pull an image from a registry
docker pull myrepo/myapp:1.0
```

---

## 12. Handy Flags Reference

| Flag | Meaning |
|---|---|
| `-d` | Run container in detached (background) mode |
| `-it` | Interactive mode with a pseudo-TTY (for shells) |
| `-p host:container` | Map a host port to a container port |
| `-v host:container` | Mount a volume or bind mount |
| `-e KEY=value` | Set an environment variable |
| `--name` | Assign a custom name to the container |
| `--rm` | Automatically remove the container when it exits |
| `--restart` | Set restart policy (`no`, `on-failure`, `always`, `unless-stopped`) |
| `-f` | Follow logs, or force an operation |
| `--network` | Attach container to a specific network |
| `-a` | Show all (used with `ps -a`, `prune -a`, etc.) |
| `--build-arg` | Pass a build-time variable to a Dockerfile |
| `--no-cache` | Skip the build cache during `docker build` |

---

## Wrapping Up

These commands cover about 95% of everyday Docker workflows — from building and running containers to managing volumes, networks, and cleaning up your system. Bookmark this as a quick reference, and once you're comfortable with these, exploring Docker Compose and Swarm will feel like a natural next step.

If you found this useful, feel free to clap, share, or drop a comment with commands you use often that aren't listed here!

**— Nilavanan S A**
