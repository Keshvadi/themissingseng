---
title: Networking in Docker
parent: Docker
nav_order: 56
layout: default
---

## Networking in Docker

Docker containers are isolated environments. By default, a container can't communicate with other containers or the outside world. Docker networking provides mechanisms for containers to communicate with each other, the host machine, and external networks.

---

## Network Types

Docker offers several network drivers, each with different characteristics and use cases.

1.  **Bridge Network (Default)**

    - **Description:** The default network driver. When you run a container without specifying a network, it's attached to the default bridge network (`bridge`). Containers on the same bridge network can communicate with each other using their _internal_ IP addresses. To access a container's services from the _host_ machine or the outside world, you need to publish ports using the `-p` or `-P` option with `docker run`.
    - **Use Case:** Suitable for running multiple containers on a single host that need to communicate with each other.
    - **Example:**

      ```bash
      docker run -d --name my_container my_image  # Run a container (attached to the default bridge)
      docker run -d -p 8080:80 --name my_web_server nginx:latest  # Run an Nginx container, mapping host port 8080 to container port 80
      ```

      _Explanation:_

      - `-d`: Runs the container in detached mode (background).
      - `--name`: Assigns a name to the container.
      - `-p 8080:80`: Publishes port 80 of the container to port 8080 on the host. You can now access the Nginx server via `http://localhost:8080`.

2.  **Host Network**

    - **Description:** The container shares the host's network stack. The container _does not_ get its own IP address. Any ports the container opens are directly accessible on the host's IP address. This provides the best network performance (no network virtualization overhead), but it can lead to port conflicts if multiple containers try to use the same port.
    - **Use Case:** When you need maximum network performance and don't need network isolation between the container and the host.
    - **Example:**

      ```bash
      docker run -d --network host --name my_container my_image
      ```

      _Note:_ Port mapping (`-p`) has no effect when using the host network.

3.  **None Network**

    - **Description:** Disables all networking for the container. The container has no external network access and cannot communicate with other containers.
    - **Use Case:** For highly isolated applications that don't require any network communication (e.g., batch processing jobs that only read and write to local files).
    - **Example:**

      ```bash
      docker run -it --network none ubuntu:22.04 bash # start ubuntu image with no network.
      ```

4.  **User-Defined Bridge Networks (Custom Bridge Networks)**

    - **Description:** Similar to the default bridge network, but you create them explicitly. The _key advantage_ of user-defined bridge networks is that they provide _automatic DNS resolution_ between containers. Containers on the same user-defined bridge network can communicate with each other using their container _names_ as hostnames.
    - **Use Case:** Recommended for most multi-container applications running on a single host. Provides better isolation and communication than the default bridge.
    - **Example:**

      ```bash
      # Create a custom bridge network
      docker network create --driver bridge my_network

      # Run two containers on the same network
      docker run -d --name web --network my_network nginx:latest
      docker run -it --name db --network my_network postgres:latest

      # From the 'web' container, you can now access the 'db' container using 'db' as the hostname:
      docker exec -it web ping db  # This will work!
      ```

      _Explanation:_

      - `docker network create`: Creates a new network.
      - `--driver bridge`: Specifies the bridge driver (optional, as it's the default).
      - `--network my_network`: Attaches the container to the `my_network` network.
      - `--name web`, `--name db`: Assigns names to the containers. These names can be used as hostnames within the `my_network` network.

5.  **Overlay Networks (Docker Swarm)**

    - **Description:** Used for multi-host networking in Docker Swarm mode (a container orchestration tool). Overlay networks allow containers running on _different_ Docker hosts to communicate seamlessly as if they were on the same network. This requires a key-value store (like Consul, etcd, or ZooKeeper) for managing the network state.
    - **Use Case:** For deploying and managing applications across a cluster of Docker hosts.
    - **Example:** (Requires a Docker Swarm setup)

      ```bash
      docker network create -d overlay --attachable my_overlay_network
      docker service create --network my_overlay_network --name my_service my_image
      ```

6.  **Macvlan Networks**

    - **Description:** Allows you to assign MAC addresses to containers, making them appear as physical devices on your network. Each container gets its own IP address directly from your network's DHCP server (or you can assign static IPs). This is useful for integrating containers with existing network infrastructure.
    - **Use Case:** When you need containers to be directly accessible on your physical network, as if they were separate physical machines. Often used for legacy applications or network monitoring tools. Requires more network configuration.
    - **Example:**

      ```bash
      # Create a macvlan network (requires configuring a parent interface and subnet)
      docker network create -d macvlan \
          --subnet=192.168.1.0/24 \
          --gateway=192.168.1.1 \
          -o parent=eth0 \
          my_macvlan_network

      # Run a container on the macvlan network
      docker run -d --name my_macvlan_container \
          --network my_macvlan_network \
          --ip 192.168.1.100 \
          my_image
      ```

      _Explanation:_

      - `-d macvlan`: Specifies the macvlan driver.
      - `--subnet`: Defines the network subnet.
      - `--gateway`: Defines the default gateway.
      - `-o parent=eth0`: Specifies the parent network interface on the host (replace `eth0` with your actual interface name).
      - `--ip`: (Optional) Assigns a static IP address to the container. If omitted, it will be requested from DHCP Server.

---

## Network Management Commands

- **`docker network ls`**

  - **Description:** Lists all available Docker networks.
  - **Example:**

        ```bash
        docker network ls
        ```

        _Sample output:_
        `     NETWORK ID     NAME             DRIVER    SCOPE

    b8e5353d129c bridge bridge local
    f39d1858d691 host host local
    e167b7c47b5a my_network bridge local
    9f42668d62f6 none null local`

- **`docker network inspect`**

  - **Description:** Displays detailed information about a specific network.
  - **Example:**

    ```bash
    docker network inspect my_network
    ```

- **`docker network create`**

  - **Description:** Creates a new Docker network.
  - **Example:**
    ```
        docker network create --driver bridge my_network
    ```

- **`docker network rm`**

  - **Description:** removes a network
  - **Example:**
    ```
      docker network rm my_network
    ```

- **`docker network connect`**

  - **Description:** Connects a _running_ container to a network. This allows you to dynamically change a container's network connectivity.
  - **Example:**

    ```bash
    docker network connect my_network my_container
    ```

- **`docker network disconnect`**

  - **Description:** Disconnects a container from a network.
  - **Example:**

    ```bash
    docker network disconnect my_network my_container
    ```

- **`docker network prune`**
  - **Description:** remove all unused networks.
  - **Example Usage:**
    ```bash
       docker network prune
    ```

---
