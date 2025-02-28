---
title: Docker Commands
parent: Docker
nav_order: 54
layout: default
---

## Docker Commands

This section covers essential Docker commands for managing images, containers, and volumes.

**Important Note:** Unless you've configured Docker to run as a non-root user (highly recommended - see the "Getting Started" section), you'll need to use `sudo` before each `docker` command.

---

### General Commands

- **`docker --help`**

  - **Description:** Displays a list of all available Docker commands and their descriptions. Use this to get help on any Docker command.
  - **Example Usage:**

    ```bash
    docker --help
    docker <command> --help  # Get help on a specific command (e.g., docker run --help)
    ```

- **`docker info`**

  - **Description:** Displays system-wide information about the Docker installation, including the number of containers and images, kernel version, and storage driver.
  - **Example Usage:**

    ```bash
    docker info
    ```

- **`docker version`**

  - **Description:** Displays the Docker version information for both the client and server.
  - **Example Usage:**
    ```bash
    docker version
    ```

---

### Image Management

- **`docker pull`**

  - **Description:** Downloads a Docker image from a registry (e.g., Docker Hub).
  - **Example Usage:**

    ```bash
    docker pull ubuntu:22.04     # Pull the Ubuntu 22.04 image
    docker pull nginx:latest      # Pull the latest version of the Nginx image
    docker pull myregistry/myimage:mytag  # Pull an image from a private registry
    ```

- **`docker images`**

  - **Description:** Lists the Docker images available on your local system.
  - **Example Usage:**

    ```bash
    docker images
    docker images -a             # Show all images (including intermediate layers)
    docker images --digests     # show image digests
    docker images --filter "dangling=true"   # show danling images
    ```

- **`docker rmi`**

  - **Description:** Removes (deletes) one or more Docker images. You cannot remove an image that is being used by a container.
  - **Example Usage:**

    ```bash
    docker rmi ubuntu:22.04       # Remove the Ubuntu 22.04 image (by tag)
    docker rmi <image_id>        # Remove an image by its ID
    docker rmi $(docker images -q) # Remove ALL images (BE CAREFUL!) - uses command substitution
    docker image prune          # remove dangling images
    docker image prune -a       # Remove all unused images
    ```

- **`docker build`**

  - **Description:** Builds a Docker image from a `Dockerfile`.
  - **Example Usage:**
    ```bash
     docker build -t my-image:latest .  # build an image and give it a name.
    ```
    _Explanation:_
    - `-t` tag the image with a human-readable name.
    - `.` build the image from the current directory.

- **`docker tag`**

  - **Description:** creates a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  - **Example Usage:**

  ```bash
    docker tag my-image:latest my-repo/my-image:v1.0 # tag an image.
  ```

- **`docker push`**
  - **Description:** pushes the image to a registry.
  - **Example Usage:**
    ```bash
      docker push my-repo/my-image:v1.0
    ```

---

### Container Management

- **`docker run`**

  - **Description:** Creates and starts a new container from a Docker image. This is one of the most important Docker commands.
  - **Example Usage:**

    ```bash
    docker run -it --name my_container ubuntu:22.04  # Run an interactive Ubuntu container
    docker run -d --name my_nginx -p 8080:80 nginx:latest  # Run an Nginx container in detached mode, mapping port 8080 on the host to port 80 in the container
    docker run -it --rm ubuntu:22.04 bash            # Run a container and automatically remove it when it exits
    docker run -v $(pwd):/app -w /app my_image python my_script.py  # Run a container with a volume mount and working directory
    docker run --env MY_VAR=my_value my_image      # Set an environment variable inside the container
    ```

  _Key Options:_

  - `-i` (`--interactive`): Keep STDIN open even if not attached (allows you to interact with the container).
  - `-t` (`--tty`): Allocate a pseudo-TTY (connects your terminal to the container's terminal). Use `-it` together for interactive sessions.
  - `-d` (`--detach`): Run the container in detached mode (in the background).
  - `--name`: Assign a name to the container.
  - `-p HOST_PORT:CONTAINER_PORT`: Publish a container's port to the host.
  - `--rm`: Automatically remove the container when it exits.
  - `-v HOST_PATH:CONTAINER_PATH`: Mount a volume (bind mount). This allows you to share files between the host and the container.
  - `-w WORKDIR`: Set the working directory inside the container.
  - `--env VAR=VALUE`: Set environment variables inside the container.

- **`docker ps`**

  - **Description:** Lists running containers.
  - **Example Usage:**

    ```bash
    docker ps         # List running containers
    docker ps -a      # List all containers (running and stopped)
    docker ps -q      # List only container IDs
    ```

- **`docker stop`**

  - **Description:** Gracefully stops a running container.
  - **Example Usage:**

    ```bash
    docker stop my_container  # Stop the container named 'my_container'
    docker stop $(docker ps -q)  # Stop all running containers
    ```

- **`docker start`**

  - **Description:** Starts a stopped container.
  - **Example Usage:**
    ```bash
    docker start my_container
    ```

- **`docker rm`**

  - **Description:** Removes (deletes) one or more _stopped_ containers.
  - **Example Usage:**

    ```bash
    docker rm my_container      # Remove the container named 'my_container'
    docker rm $(docker ps -a -q) # Remove ALL containers (BE CAREFUL!)
    docker container prune      # remove all stopped containers
    ```

- **`docker exec`**

  - **Description:** Runs a command _inside_ a running container. Very useful for debugging and interacting with a running container.
  - **Example Usage:**

    ```bash
    docker exec -it my_container bash  # Open an interactive shell inside 'my_container'
    docker exec my_container ls -l /app # List the contents of the /app directory inside the container
    ```

- **`docker logs`**

  - **Description:** displays the logs of a container.
  - **Example Usage:**
    ```bash
      docker logs my_container # displays the logs
      docker logs -f my_container # real time logs
    ```

---

### Volume Management

- **`docker volume ls`**

  - **Description:** list all volumes.
  - **Example Usage:**

    ```bash
       docker volume ls
    ```

- **`docker volume create`**
  - **Description:** create a volume.
  - **Example Usage:**
    ```bash
       docker volume create my_volume
    ```
- **`docker volume rm`**
  - **Description:** Remove a volume.
  - **Example Usage:**
    ```bash
       docker volume rm my_volume
    ```
- **`docker volume prune`**
  - **Description:** Remove all unused volumes.
  - **Example Usage:**
    ```bash
       docker volume prune
    ```

---

### Copying Files

<<<<<<< HEAD

- **Copy a file from container to local host**
  ```bash
  docker cp my_container:usr/src/project/file .
  ```
- **Copy a file from local host to container**
  ```bash
  docker cp file my_container:/usr/src/project
  ```
  =======

* **`docker cp`**

  - **Description:** Copies files/directories between a container and the local filesystem.
  - **Example Usage:**

    ```bash
    docker cp my_container:/path/in/container /local/path  # Copy *from* container *to* host
    docker cp /local/path my_container:/path/in/container  # Copy *from* host *to* container
    ```

---

> > > > > > > 5eb2d5e (updated content)
