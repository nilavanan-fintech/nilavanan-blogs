# Top 100 Docker Interview Questions & Answers

*Compiled by Nilavanan S A*

A categorized list of the most commonly asked Docker interview questions — from basics to advanced orchestration — with concise answers to help you prepare quickly.

---

## Table of Contents

1. [Docker Basics](#1-docker-basics)
2. [Docker Architecture](#2-docker-architecture)
3. [Docker Images](#3-docker-images)
4. [Docker Containers](#4-docker-containers)
5. [Dockerfile](#5-dockerfile)
6. [Docker Volumes & Storage](#6-docker-volumes--storage)
7. [Docker Networking](#7-docker-networking)
8. [Docker Compose](#8-docker-compose)
9. [Docker Swarm & Orchestration](#9-docker-swarm--orchestration)
10. [Docker Security](#10-docker-security)
11. [Docker Registry & Hub](#11-docker-registry--hub)
12. [Troubleshooting & Miscellaneous](#12-troubleshooting--miscellaneous)

---

## 1. Docker Basics

**1. What is Docker?**
Docker is an open-source platform that packages applications and their dependencies into lightweight, portable containers, ensuring consistent behavior across environments.

**2. What problem does Docker solve?**
It eliminates the "it works on my machine" problem by packaging code, runtime, libraries, and configs together, ensuring consistency across dev, test, and production.

**3. What is a container?**
A lightweight, standalone, executable unit that packages application code with all its dependencies, sharing the host OS kernel.

**4. How is Docker different from a virtual machine?**
VMs virtualize hardware and run a full guest OS per instance; containers virtualize the OS and share the host kernel, making them faster and lighter.

**5. What are the main components of Docker?**
Docker Engine, Docker Client, Docker Daemon, Docker Images, Docker Containers, Docker Registry, and Docker Compose.

**6. What is Docker Engine?**
The core client-server application consisting of the Docker Daemon (`dockerd`), REST API, and CLI that builds and runs containers.

**7. What operating systems support Docker?**
Linux natively; Windows and macOS via Docker Desktop, which uses a lightweight VM to run the Linux kernel.

**8. What is containerization?**
The process of packaging software along with its dependencies so it can run reliably across different computing environments.

**9. What are the benefits of using Docker?**
Portability, faster deployment, consistent environments, resource efficiency, easy scaling, and simplified CI/CD pipelines.

**10. What is the difference between Docker and Kubernetes?**
Docker builds and runs containers; Kubernetes orchestrates and manages containers at scale across clusters (scheduling, scaling, self-healing).

---

## 2. Docker Architecture

**11. Explain Docker's client-server architecture.**
The Docker Client sends commands to the Docker Daemon via REST API/socket; the Daemon manages images, containers, networks, and volumes.

**12. What is the Docker Daemon?**
A background process (`dockerd`) that listens for API requests and manages Docker objects like images, containers, and volumes.

**13. What is containerd?**
A high-level container runtime that manages the container lifecycle (start, stop, pause) and is used internally by Docker.

**14. What is runc?**
A low-level, lightweight CLI tool for spawning and running containers according to the OCI (Open Container Initiative) specification.

**15. What is the Docker CLI?**
The command-line tool (`docker`) users interact with to issue commands like `docker run`, `docker build`, and `docker ps`.

**16. What is the Docker REST API?**
An API that the Docker CLI and other tools use to communicate with the Docker Daemon programmatically.

**17. What namespaces does Docker use for isolation?**
PID, Network, Mount, UTS, IPC, and User namespaces — each isolating a different aspect of the container's view of the system.

**18. What are cgroups and why does Docker use them?**
Control groups limit and monitor resource usage (CPU, memory, disk I/O) per container, preventing one container from starving others.

**19. What is the Union File System in Docker?**
A layered filesystem (e.g., OverlayFS) that stacks image layers and adds a writable layer on top for the container, enabling efficient storage.

**20. What is OCI (Open Container Initiative)?**
An industry standard that defines specifications for container image formats and runtimes, ensuring interoperability across tools.

---

## 3. Docker Images

**21. What is a Docker image?**
A read-only, immutable template containing application code, dependencies, and configuration used to create containers.

**22. How do you build a Docker image?**
Using `docker build -t <name>:<tag> .` with a Dockerfile in the build context.

**23. What is an image layer?**
Each instruction in a Dockerfile creates a layer; layers are cached and stacked to form the final image, improving reusability and build speed.

**24. How do you list all images on a system?**
`docker images` or `docker image ls`.

**25. How do you remove a Docker image?**
`docker rmi <image_id>`.

**26. What is image tagging?**
Assigning a human-readable label (e.g., `myapp:1.0`) to an image for version control and identification.

**27. What's the difference between `docker save` and `docker export`?**
`docker save` exports an image (with layers/history) to a tar file; `docker export` exports a container's filesystem as a flat tar, losing history.

**28. What is a base image?**
The starting image specified in `FROM` that your custom image builds upon (e.g., `ubuntu`, `alpine`, `node`).

**29. Why is Alpine Linux popular as a base image?**
It's extremely lightweight (~5MB), reducing image size and attack surface compared to full OS distributions.

**30. How do you reduce Docker image size?**
Use minimal base images, multi-stage builds, combine RUN commands, remove unnecessary files, and use `.dockerignore`.

**31. What is a multi-stage build?**
A Dockerfile technique using multiple `FROM` statements to separate build and runtime environments, keeping the final image small.

**32. How do you inspect an image's metadata?**
`docker inspect <image_id>`.

**33. What is image caching in Docker builds?**
Docker reuses unchanged layers from previous builds instead of rebuilding them, speeding up subsequent builds.

**34. How do you view the history/layers of an image?**
`docker history <image_id>`.

**35. What is a "dangling image"?**
An image layer with no tag, usually left behind after rebuilding an image with the same tag; shown as `<none>` in `docker images`.

---

## 4. Docker Containers

**36. What is a Docker container?**
A running (or stopped) instance of a Docker image with its own writable layer, process space, and network interface.

**37. How do you run a container?**
`docker run <image_name>`, with flags like `-d` (detached), `-p` (port mapping), `-v` (volume), `--name` (container name).

**38. How do you list running containers?**
`docker ps` (add `-a` to include stopped containers).

**39. How do you stop and start a container?**
`docker stop <container_id>` and `docker start <container_id>`.

**40. How do you remove a container?**
`docker rm <container_id>` (use `-f` to force-remove a running container).

**41. What's the difference between `docker stop` and `docker kill`?**
`stop` sends SIGTERM (graceful shutdown, then SIGKILL after a timeout); `kill` sends SIGKILL immediately.

**42. How do you access a running container's shell?**
`docker exec -it <container_id> /bin/bash` (or `/bin/sh` for minimal images).

**43. How do you view container logs?**
`docker logs <container_id>` (add `-f` to follow in real time).

**44. What happens to data when a container is deleted?**
Any data in the container's writable layer is lost unless it was stored in a volume or bind mount.

**45. What is the difference between `docker run` and `docker start`?**
`run` creates a new container from an image; `start` restarts an existing (stopped) container.

**46. How do you copy files between host and container?**
`docker cp <src> <container_id>:<dest>` and vice versa.

**47. What is a container's PID 1 process?**
The main process defined by `CMD`/`ENTRYPOINT`; if it exits, the container stops.

**48. How do you limit a container's CPU and memory usage?**
Using flags like `--memory`, `--cpus`, e.g., `docker run --memory=512m --cpus=1 myapp`.

**49. What is container restart policy?**
A setting (`--restart`) controlling whether Docker restarts a container automatically — options: `no`, `on-failure`, `always`, `unless-stopped`.

**50. Can a single image spawn multiple containers?**
Yes — each `docker run` creates an independent container instance from the same image, each with isolated state.

---

## 5. Dockerfile

**51. What is a Dockerfile?**
A text file containing a set of instructions used to build a Docker image automatically.

**52. What is the difference between `CMD` and `ENTRYPOINT`?**
`CMD` provides default arguments that can be overridden at runtime; `ENTRYPOINT` defines a fixed executable that always runs, with `CMD` supplying default args to it.

**53. What is the difference between `COPY` and `ADD`?**
`COPY` simply copies files/directories; `ADD` also supports remote URLs and auto-extracts compressed archives.

**54. What does the `WORKDIR` instruction do?**
Sets the working directory for subsequent instructions (`RUN`, `CMD`, `COPY`) inside the image.

**55. What does `EXPOSE` do in a Dockerfile?**
Documents which port the container listens on; it doesn't actually publish the port (that's done via `-p` at runtime).

**56. What is `ENV` used for?**
Sets environment variables inside the image, available during build and at container runtime.

**57. What is `ARG` and how is it different from `ENV`?**
`ARG` defines build-time-only variables passed via `--build-arg`; `ENV` variables persist into the running container.

**58. What is `.dockerignore`?**
A file listing paths to exclude from the build context, reducing build time and image size and preventing sensitive files from being copied in.

**59. What does `RUN` do vs `CMD`?**
`RUN` executes commands at build time to create layers (e.g., installing packages); `CMD` specifies the default command executed when the container starts.

**60. How do you set a non-root user in a Dockerfile?**
Using `USER <username>` after creating the user with `RUN useradd ...`, improving container security.

**61. What is the build context in `docker build`?**
The set of files (from the specified directory) sent to the Docker daemon, which can be referenced by `COPY`/`ADD` instructions.

**62. How can you pass environment variables to a Dockerfile at build time?**
Using `ARG` in the Dockerfile and `--build-arg key=value` in the `docker build` command.

**63. What is `HEALTHCHECK` in a Dockerfile?**
An instruction defining a command Docker runs periodically to verify the container is functioning correctly.

**64. Why should you avoid running `apt-get update` and `apt-get install` in separate `RUN` layers?**
Separating them can cache a stale `update` layer, leading to installing outdated/broken packages later; combine them in one `RUN`.

**65. What is the best practice for ordering Dockerfile instructions?**
Place rarely changing instructions (like installing dependencies) earlier and frequently changing instructions (like copying source code) later, to maximize layer caching.

---

## 6. Docker Volumes & Storage

**66. What is a Docker volume?**
A persistent storage mechanism managed by Docker, stored outside the container's writable layer, surviving container deletion.

**67. What's the difference between a volume and a bind mount?**
Volumes are managed by Docker and stored in Docker's storage area; bind mounts map an exact host path into the container, giving direct host filesystem access.

**68. How do you create and use a volume?**
`docker volume create myvolume`, then `docker run -v myvolume:/app/data myimage`.

**69. How do you list and remove volumes?**
`docker volume ls` and `docker volume rm <volume_name>` (`docker volume prune` removes unused ones).

**70. What is a tmpfs mount?**
A mount stored in the host's memory only (not on disk), useful for sensitive or temporary data that shouldn't persist.

**71. Why use volumes instead of storing data inside the container?**
Data in a container's writable layer is lost when the container is removed; volumes decouple data lifecycle from the container lifecycle.

**72. Can multiple containers share the same volume?**
Yes, multiple containers can mount and share the same named volume simultaneously.

**73. What is the default storage driver in Docker?**
OverlayFS (`overlay2`) is the recommended and most commonly used storage driver on modern Linux systems.

---

## 7. Docker Networking

**74. What are the default network types in Docker?**
Bridge, Host, None, and Overlay (for Swarm).

**75. What is the bridge network?**
The default network mode where containers get an internal IP and communicate via a virtual bridge, with ports optionally published to the host.

**76. What is host networking mode?**
The container shares the host's network stack directly, with no isolation or port mapping needed — used for max performance.

**77. What is the "none" network mode?**
Completely disables networking for the container, isolating it from all network access.

**78. How do containers communicate with each other by name?**
Via Docker's embedded DNS on user-defined bridge networks, where containers can resolve each other by container name/alias.

**79. How do you publish a container's port to the host?**
Using `-p <host_port>:<container_port>` in `docker run`.

**80. What is an overlay network?**
A multi-host network type used in Docker Swarm that allows containers on different hosts to communicate securely.

**81. How do you create a custom network?**
`docker network create mynetwork`, then attach containers with `--network mynetwork`.

**82. How do you inspect a Docker network?**
`docker network inspect <network_name>`.

---

## 8. Docker Compose

**83. What is Docker Compose?**
A tool for defining and running multi-container applications using a single YAML file (`docker-compose.yml`).

**84. How do you start services defined in a compose file?**
`docker compose up` (add `-d` for detached mode).

**85. How do you stop and remove all compose-managed containers?**
`docker compose down` (add `-v` to also remove volumes).

**86. What are the key sections of a `docker-compose.yml` file?**
`services`, `networks`, `volumes`, and optionally `configs`/`secrets`.

**87. How does Compose handle networking between services?**
It automatically creates a default network where services can reach each other by their service name.

**88. What is the difference between `docker-compose.yml` and `docker-compose.override.yml`?**
The override file automatically merges with the base file to customize settings (e.g., for local dev) without editing the original.

**89. How do you scale a service using Compose?**
`docker compose up --scale <service_name>=<count>`.

**90. Can Docker Compose be used in production?**
It can, but for large-scale, resilient production deployments, orchestrators like Kubernetes or Docker Swarm are generally preferred.

---

## 9. Docker Swarm & Orchestration

**91. What is Docker Swarm?**
Docker's native clustering and orchestration tool that turns a group of Docker hosts into a single virtual host (a "swarm").

**92. What is the difference between a Swarm manager and worker node?**
Managers handle orchestration, scheduling, and cluster state; workers execute the actual containerized tasks assigned by managers.

**93. What is a "service" in Docker Swarm?**
A definition of tasks (containers) to run across the swarm, including image, replicas, and update policy.

**94. How do you initialize a swarm?**
`docker swarm init`.

**95. What is a "stack" in Docker Swarm?**
A collection of services deployed together, usually defined via a Compose file and deployed with `docker stack deploy`.

**96. How does Swarm handle load balancing?**
Through an internal routing mesh that distributes incoming requests across all nodes running a given service's replicas.

**97. How does Docker Swarm differ from Kubernetes?**
Swarm is simpler and tightly integrated with Docker CLI/Compose; Kubernetes offers more advanced scheduling, scaling, and ecosystem tooling but has a steeper learning curve.

---

## 10. Docker Security

**98. What are some Docker security best practices?**
Run containers as non-root users, use minimal base images, scan images for vulnerabilities, limit container capabilities, keep Docker updated, and avoid exposing the Docker socket unnecessarily.

**99. What is Docker Content Trust?**
A feature that enables image signing and verification, ensuring only trusted, signed images are pulled and run.

---

## 11. Docker Registry & Hub

**100. What is a Docker Registry, and how is it different from Docker Hub?**
A registry is a storage/distribution system for Docker images (public or private); Docker Hub is Docker's own public, hosted registry service. Organizations can also run private registries for internal image management.

---

## 12. Troubleshooting & Miscellaneous

**Bonus: How do you debug a container that keeps exiting immediately?**
Check logs with `docker logs <container_id>`, verify the `CMD`/`ENTRYPOINT` process isn't exiting on its own, and try running interactively with `docker run -it <image> sh` to inspect manually.

**Bonus: How do you clean up unused Docker resources?**
`docker system prune` removes stopped containers, unused networks, dangling images, and build cache (`-a` removes all unused images too).

---

*Good luck with your interview! If you found this useful, feel free to share it or drop a comment with questions you've been asked that aren't on this list.*

**— Nilavanan S A**
