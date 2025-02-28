---
title: Getting Started with Docker
parent: Docker
nav_order: 52
layout: default
---

## Installation

This section guides you through installing Docker on various operating systems. We'll focus on Ubuntu Linux, but provide links for Windows and macOS installations.

- [Windows Installation](https://docs.docker.com/desktop/install/windows-install/)
- [macOS Installation](https://docs.docker.com/desktop/install/mac-install/)

---

## Linux (Ubuntu)

These instructions are specifically for Ubuntu. For other Linux distributions, refer to the official Docker documentation: [Install Docker Engine](https://docs.docker.com/engine/install/).

**Steps:**

1.  **Set up Docker's `apt` repository:** This allows your system to download and install official Docker packages.

    ```bash
    # Update the apt package index and install packages to allow apt to use a repository over HTTPS:
    sudo apt-get update
    sudo apt-get install -y ca-certificates curl gnupg

    # Create a directory for the keyring (if it doesn't exist)
    sudo install -m 0755 -d /etc/apt/keyrings

    # Download Docker's official GPG key and add it to the keyring:
    curl -fsSL [https://download.docker.com/linux/ubuntu/gpg](https://download.docker.com/linux/ubuntu/gpg) | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

    # Set permissions on the key file
    sudo chmod a+r /etc/apt/keyrings/docker.gpg

    # Add the repository to Apt sources:
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] [https://download.docker.com/linux/ubuntu](https://download.docker.com/linux/ubuntu) \
      $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

    # Update the apt package index again:
    sudo apt-get update
    ```

    _Explanation:_

    - `apt-get update`: Updates the local package index.
    - `apt-get install -y ca-certificates curl gnupg`: Installs required packages (`-y` automatically answers "yes" to prompts).
    - `install -m 0755 -d /etc/apt/keyrings`: Creates the `/etc/apt/keyrings` directory with correct permissions.
    - `curl ... | sudo gpg --dearmor ...`: Downloads Docker's GPG key, dearmors it (converts it to a binary format), and saves it.
    - `chmod a+r ...`: Sets read permissions on the key file.
    - `echo ... | sudo tee ...`: Adds the Docker repository to your system's list of software sources.
    - `$(lsb_release -cs)`: gets your ubuntu version's codename.

2.  **Install Docker Engine:**

    ```bash
    sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```

    _Explanation:_
    \*Installs packages for docker.

3.  **Verify Installation:**

    ```bash
    sudo docker run hello-world
    ```

    _Sample Output (truncated):_

    ```
    Unable to find image 'hello-world:latest' locally
    latest: Pulling from library/hello-world
    ...
    Status: Downloaded newer image for hello-world:latest

    Hello from Docker!
    This message shows that your installation appears to be working correctly.
    ...
    ```

    This command downloads a test image ("hello-world") and runs it in a container. If you see the "Hello from Docker!" message, your installation is working.

4.  **(Optional, but Recommended) Manage Docker as a Non-Root User:**

    By default, you need to use `sudo` to run Docker commands. To avoid this, add your user to the `docker` group:

    ```bash
    sudo usermod -aG docker $USER
    ```

    _Important:_ You'll need to **log out and log back in** (or run `newgrp docker`) for this change to take effect. After logging back in, you should be able to run `docker` commands without `sudo`.

    Refer to the official Docker documentation for more details on post-installation steps for Linux: [Linux Post-Installation](https://docs.docker.com/engine/install/linux-postinstall/)

---
