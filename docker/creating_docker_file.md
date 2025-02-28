---
title: Dockerfile Creation
parent: Docker
nav_order: 55
layout: default
---

## Dockerfile Creation

A `Dockerfile` is a text file that contains instructions for building a Docker image. It's like a recipe: it specifies the base operating system, dependencies, commands to execute, and the application code to include. Docker uses the `Dockerfile` to automate the image creation process.

---

## Dockerfile Instructions

Here are some of the most common `Dockerfile` instructions:

### `FROM`

- **Description:** Specifies the base image for your new image. _Every_ `Dockerfile` must start with a `FROM` instruction.
- **Example:**

  ```dockerfile
  FROM ubuntu:22.04  # Use the official Ubuntu 22.04 image as the base
  FROM python:3.9-slim # Use a slim Python 3.9 image
  FROM scratch       # Create an empty image
  ```

---

### `WORKDIR`

- **Description:** Sets the working directory _inside_ the image. Subsequent `RUN`, `COPY`, `ADD`, `CMD`, and `ENTRYPOINT` instructions will be executed in this directory. It's like using `cd` in a shell script. If the directory doesn't exist, it will be created.
- **Example:**

  ```dockerfile
  WORKDIR /app  # Set the working directory to /app
  ```

---

### `COPY`

- **Description:** Copies files and directories from the _host_ machine (where you're running `docker build`) into the _image_.
- **Example:**

  ```dockerfile
  COPY requirements.txt /app/  # Copy requirements.txt to the /app directory in the image
  COPY src/ /app/src/         # Copy the entire 'src' directory to /app/src/
  COPY . /app                # Copy everything from the current directory to /app (be careful with this!)
  ```

  _Note:_ It's best practice to be specific about what you copy. Copying everything (`COPY . /app`) can lead to larger image sizes and potential security issues if you accidentally include sensitive files. Use a `.dockerignore` file (similar to `.gitignore`) to exclude files and directories from the build context.

---

### `ADD`

- **Description:** Similar to `COPY`, but with additional features:
  - Can copy files from URLs.
  - Can automatically extract compressed archives (tar, gzip, bzip2, etc.).
- **Example:**
  ```dockerfile
  ADD [https://example.com/my_app.tar.gz](https://www.google.com/search?q=https://example.com/my_app.tar.gz) /tmp/
  ```

---
