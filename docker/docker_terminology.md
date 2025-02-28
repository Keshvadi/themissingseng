---
title: Docker Terminology
parent: Docker
nav_order: 51
layout: default
---

## Docker Terminology

This section introduces the core concepts and terminology used in Docker. Understanding these terms is essential for working with Docker effectively.

---

## Docker Architecture

Docker's architecture is client-server based. The key components are:

### Docker Engine

The Docker Engine is the core of Docker, responsible for building and running containers. It consists of:

- **Docker Daemon (`dockerd`):** A persistent background process that manages Docker objects (images, containers, networks, volumes). The daemon listens for requests from the Docker CLI or other clients via the Docker API.
- **Docker CLI (Command-Line Interface):** The primary way users interact with Docker. You use commands like `docker run`, `docker build`, etc., to interact with the daemon.
- **Docker REST API:** An API that allows tools and applications to interact with the Docker daemon programmatically. The Docker CLI uses this API.

### Docker Objects

- **Images:** Read-only templates used to create containers. Think of an image as a snapshot of a file system and application configuration. Images are built from a `Dockerfile` (see below). Images are _layered_, meaning they are built up from a series of read-only layers, which promotes efficiency and reusability.
- **Containers:** Running instances of Docker images. They are isolated environments that contain everything needed to run an application. Containers are lightweight and share the host operating system's kernel.
- **Volumes:** Persistent data storage for containers. Volumes are _independent_ of the container lifecycle, meaning data in a volume persists even if the container is stopped or deleted. Volumes are the preferred way to store persistent data in Docker. They can be shared by multiple containers.
- **Networks:** Enable communication between containers, and between containers and the outside world. Docker provides different network drivers for various use cases (e.g., bridge networks for connecting containers on the same host, overlay networks for connecting containers across multiple hosts).
- **Registries**: Repositories for storing and sharing docker images. Examples are DockerHub, AWS ECR and self-hosted registries.

### Dockerfile

- **Description:** A text file that contains instructions for building a Docker image. Each instruction in a `Dockerfile` creates a new layer in the image.
- **Key Instructions:**
  - `FROM`: Specifies the base image (e.g., `FROM ubuntu:22.04`).
  - `RUN`: Executes a command (e.g., `RUN apt-get update && apt-get install -y python3`).
  - `COPY`: Copies files from the host machine into the image.
  - `ADD`: Similar to `COPY`, but can also handle URLs and extract archives.
  - `WORKDIR`: Sets the working directory inside the image.
  - `ENV`: Sets environment variables.
  - `EXPOSE`: Informs Docker that the container listens on the specified network ports at runtime (doesn't actually publish the ports).
  - `CMD`: Specifies the command to run when the container starts. There can be only one `CMD` instruction (or it will be overridden).
  - `ENTRYPOINT`: Similar to `CMD`, but designed to be the main command of the container. `CMD` arguments can be appended to `ENTRYPOINT`.

### Docker Compose

- **Description:** A tool for defining and managing multi-container Docker applications. You define your application's services, networks, and volumes in a `docker-compose.yml` file (YAML format). This makes it easy to start, stop, and manage complex applications with a single command.

**Example `docker-compose.yml`:**

```yaml
version: "3.9"
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
  db:
    image: postgres:14
    environment:
      POSTGRES_PASSWORD: mysecretpassword
    volumes:
      - db_data:/var/lib/postgresql/data
volumes:
  db_data:
```
