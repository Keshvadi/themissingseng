---
title: Installation
nav_order: 99
has_children: false
layout: default
---

## Running Ubuntu in Docker (for Practice)

This webbook covers many command-line tools and concepts. The easiest way to follow along and practice is to use a consistent environment. We'll use a Docker container running Ubuntu Linux for this purpose. This allows you to experiment without affecting your host operating system.

**Prerequisites:**

- Docker Desktop installed and running on your system (Windows, macOS, or Linux). See the [Docker installation instructions](https://docs.docker.com/get-docker/) for your operating system.

**Steps:**

1.  **Start an Interactive Ubuntu Container:**

    Open a terminal (Command Prompt or PowerShell on Windows, Terminal on macOS/Linux) and run the following command:

    ```bash
    docker run -it --rm ubuntu:22.04 bash
    ```

    _Explanation:_

    - `docker run`: This command creates and starts a new container.
    - `-it`: This is a combination of two options:
      - `-i` (`--interactive`): Keeps STDIN open, allowing you to interact with the container.
      - `-t` (`--tty`): Allocates a pseudo-TTY, which gives you a terminal interface.
    - `--rm`: This option automatically _removes_ the container when you exit it. This is very convenient for temporary testing environments, as it prevents the buildup of stopped containers.
    - `ubuntu:22.04`: This specifies the Docker image to use. We're using the official Ubuntu 22.04 image from Docker Hub.
    - `bash`: This specifies the command to run _inside_ the container when it starts. In this case, we're starting a Bash shell, giving you a command-line prompt within the Ubuntu container.

    After running this command, you'll be _inside_ the Ubuntu container's shell. Your prompt will likely change to something like `root@<container_id>:/#`.

2.  **Update and Prepare the Container (Optional, but Recommended):**

    Inside the container, run the following commands:

    ```bash
    apt update  # Update the package list
    apt upgrade -y # Upgrade the installed packages
    apt install -y --no-install-recommends unminimize nano g++ telnet python3 python3-pip net-tools iputils-ping tcpdump
    ```

    _Explanation:_

    - `apt update`: Updates the list of available packages. _Always_ run this before installing new packages.
    - `apt upgrade -y`: Upgrades all installed packages to their latest versions.
    - `apt install -y --no-install-recommends ...`: Installs the necessary tools for the webbook exercises:
    - `--no-install-recommends`: Installs only essential dependencies, keeping the image size down.
    - `unminimize`: Restores some packages that are removed in the minimal Ubuntu base image.
      - `nano`: A simple text editor.
      - `g++`: The GNU C++ compiler.
      - `telnet`: A basic network utility (useful for testing network connectivity – though often replaced by `netcat` or `nmap`).
      - `python3`: The Python 3 interpreter.
      - `python3-pip`: The package installer for Python.
      - `net-tools`: Provides ifconfig command.
      - `iputils-ping`: Provides the `ping` command.
      - `tcpdump`: A network packet analyzer.
    - `-y`: Automatically answers "yes" to any prompts during installation.

3.  **Open Additional Terminals (Optional):**

If you need to run multiple commands simultaneously or have multiple shells open to the _same_ container, you can use `docker exec`.

- First, find the container ID or name. While inside the container, you can usually see the container ID in the prompt. You can also run `docker ps` in a _separate_ terminal (on your host machine) to list running containers:

  ```bash
  docker ps
  # CONTAINER ID   IMAGE          COMMAND    CREATED       STATUS       PORTS     NAMES
  # a1b2c3d4e5f6   ubuntu:22.04   "bash"     2 minutes ago Up 2 minutes             my_ubuntu
  ```

- Then, use `docker exec` to open a new shell in the running container:

  ```bash
    docker exec -it a1b2c3d4e5f6 bash  # Use the container ID or name
    # OR
    docker exec -it my_ubuntu bash
  ```

  This command opens a _new_ interactive Bash shell (`-it bash`) inside the running container (`a1b2c3d4e5f6` or `my_ubuntu`). You'll have two separate terminals connected to the same container.

4.  **Exiting the Container:**

    To exit the container, simply type `exit` at the container's shell prompt. Because we used the `--rm` option when starting the container, the container will be automatically deleted when you exit.

---

## Windows (Alternative Approach)

If you're using Windows and prefer not to use Docker Desktop, you can use Windows Subsystem for Linux (WSL) to run a Linux distribution (like Ubuntu) directly on Windows. This provides a native Linux environment without the overhead of a virtual machine.

- [Run Linux containers on Windows](https://ubuntu.com/tutorials/windows-ubuntu-hyperv-containers#1-overview) (using Hyper-V containers – this is still within a container).
- [Install WSL](https://learn.microsoft.com/en-us/windows/wsl/install) (using WSL 2 – this runs a full Linux kernel). This is generally the _recommended_ approach for development on Windows.

Once WSL is set up, you can install the necessary tools (Git, Docker, etc.) within the Linux distribution, just as you would on a native Linux system.

---
