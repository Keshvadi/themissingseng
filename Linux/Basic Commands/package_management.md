---
title: Package Management
parent: Basic Commands
nav_order: 23
layout: default
---

## Package Management in Linux

Package management is crucial for installing, updating, removing, and managing software on a Linux system. This section covers essential commands, focusing primarily on Debian/Ubuntu systems (using `apt` and `dpkg`). We'll also briefly mention package management on CentOS/Fedora.

---

### `apt update`

- **Description:** Updates the local package index. This _doesn't_ install or upgrade any packages; it simply refreshes the list of available packages and their versions from the configured repositories. **Always run this before `apt upgrade`**.
- **Example Usage:**

  ```bash
  sudo apt update
  ```

  _Sample Output (truncated - it will show a lot of "Get" lines):_

  ```
  ...
  Get:1 [http://archive.ubuntu.com/ubuntu](http://archive.ubuntu.com/ubuntu) jammy InRelease [270 kB]
  Get:2 [http://archive.ubuntu.com/ubuntu](http://archive.ubuntu.com/ubuntu) jammy-updates InRelease [119 kB]
  ...
  Fetched 4,837 kB in 3s (1,612 kB/s)
  Reading package lists... Done
  Building dependency tree... Done
  Reading state information... Done
  12 packages can be upgraded. Run 'apt list --upgradable' to see them.
  ```

---

### `apt upgrade`

- **Description:** Upgrades all installed packages to their newest available versions (based on the updated package index from `apt update`).
- **Example Usage:**

  ```bash
  sudo apt upgrade
  ```

  _Sample Output (truncated):_

  ```
    Reading package lists... Done
    Building dependency tree... Done
    Reading state information... Done
    Calculating upgrade... Done
    The following packages will be upgraded:
     ... (list of packages) ...
    12 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
    Need to get 1,234 KB of archives.
    After this operation, 5,678 kB of additional disk space will be used.
    Do you want to continue? [Y/n] y
  ```

  _Note:_ It's generally good practice to run `sudo apt update` before `sudo apt upgrade`.

---

### `apt install`

- **Description:** Installs a new package (or multiple packages).
- **Example Usage:**

  ```bash
  sudo apt install package_name     # Installs a single package
  sudo apt install package1 package2 package3  # Installs multiple packages
  sudo apt install code             # Installs Visual Studio Code (if available in the repository)
  ```

  _Sample Output (truncated):_

  ```
  Reading package lists... Done
  Building dependency tree... Done
  Reading state information... Done
  The following NEW packages will be installed:
    code
  0 upgraded, 1 newly installed, 0 to remove and 12 not upgraded.
  Need to get 85.4 MB of archives.
  After this operation, 345 MB of additional disk space will be used.
  Do you want to continue? [Y/n] y
  ...
  ```

  _Note:_ As you correctly pointed out, `apt` is generally preferred over `apt-get` for interactive use. `apt-get` is still useful in scripts for its more predictable behavior.

---

### `dpkg -i`

- **Description:** Installs a local `.deb` package file (Debian package). This is used when you've _downloaded_ a package file directly (e.g., from a website) rather than from a repository.
- **Example Usage:**

  ```bash
  sudo dpkg -i package_file.deb  # Installs the .deb file
  ```

  _Important Note:_ `dpkg` does _not_ automatically handle dependencies. If the `.deb` file requires other packages that aren't installed, the installation will fail. You might need to use `sudo apt install -f` (fix broken) after `dpkg -i` to resolve dependencies:

  ```bash
  sudo apt install -f  # Attempts to fix broken dependencies after a dpkg installation.
  ```

---

### `apt remove`

- **Description:** Removes an installed package. This leaves behind configuration files.
- **Example Usage:**

  ```bash
  sudo apt remove package_name
  ```

  _Sample Output (truncated):_

  ```
  Reading package lists... Done
  Building dependency tree... Done
  Reading state information... Done
  The following packages will be REMOVED:
    package_name
  0 upgraded, 0 newly installed, 1 to remove and 12 not upgraded.
  After this operation, 1,234 kB disk space will be freed.
  Do you want to continue? [Y/n] y
    ...
  ```

---

### `apt purge`

- **Description:** Removes an installed package _and_ its associated configuration files. This provides a cleaner removal.
- **Example Usage:**

  ```bash
  sudo apt purge package_name
  ```

  _Sample Output (truncated):_

  ```
  Reading package lists... Done
  Building dependency tree... Done
  Reading state information... Done
  The following packages will be REMOVED:
    package_name*
  0 upgraded, 0 newly installed, 1 to remove and 12 not upgraded.
  After this operation, 1,234 kB disk space will be freed.
  Do you want to continue? [Y/n] y
  ...
  (Reading database ... 123456 files and directories currently installed.)
  Removing package_name (1.2.3-4ubuntu5) ...
  Purging configuration files for package_name (1.2.3-4ubuntu5) ...
  ...
  ```

  _Note:_ The asterisk (`*`) after the package name in the output indicates that configuration files will also be removed.

---

### `apt autoremove`

- **Description:** Removes automatically installed packages that are no longer needed (dependencies that were installed for other packages that have since been removed). This helps keep your system clean.
- **Example Usage:**

  ```bash
  sudo apt autoremove
  ```

  _Sample Output (truncated):_

  ```
    Reading package lists... Done
    Building dependency tree... Done
    Reading state information... Done
    The following packages will be REMOVED:
      dependency1 dependency2
    0 upgraded, 0 newly installed, 2 to remove and 12 not upgraded.
    After this operation, 4,567 kB disk space will be freed.
    Do you want to continue? [Y/n] y
    ...
  ```

---

### `apt list --installed`

- **Description:** Lists all installed packages. Provides a more concise output than `dpkg --list`.
- **Example Usage:**

  ```bash
  apt list --installed
  ```

  _Sample Output (truncated - it will be a long list!):_

  ```
  Listing... Done
  accountsservice/jammy-updates,now 22.07.5-2ubuntu1.2 amd64 [installed,automatic]
  acl/jammy,now 2.3.1-1 amd64 [installed,automatic]
  adduser/jammy,now 3.129ubuntu1 all [installed]
  ...
  ```

---

### `dpkg --list`

- **Description**: Lists all installed packages including detailed information.
- **Example Usage:**

  ```bash
  dpkg --list
  ```

---

### Package Management on CentOS/Fedora (Brief Overview)

CentOS and Fedora use `yum` (older versions) or `dnf` (newer versions) as their package manager. Here are the equivalent commands:

| Debian/Ubuntu (`apt`)    | CentOS/Fedora (`yum`/`dnf`)                         |
| ------------------------ | --------------------------------------------------- |
| `sudo apt update`        | `sudo yum check-update` / `sudo dnf check-update`   |
| `sudo apt upgrade`       | `sudo yum update` / `sudo dnf upgrade`              |
| `sudo apt install <pkg>` | `sudo yum install <pkg>` / `sudo dnf install <pkg>` |
| `sudo apt remove <pkg>`  | `sudo yum remove <pkg>` / `sudo dnf remove <pkg>`   |
| `sudo apt autoremove`    | `sudo yum autoremove` / `sudo dnf autoremove`       |
| `apt list --installed`   | `yum list installed` / `dnf list installed`         |

_Note: `dnf` is the modern replacement for `yum` and is generally preferred on newer Fedora and CentOS systems._

---
