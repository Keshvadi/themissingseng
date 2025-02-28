---
title: User Management
parent: Advanced Commands
nav_order: 32
layout: default
---

## User Management in Linux

User management is a crucial aspect of system administration in Linux, allowing you to control access and permissions for different users on the system. This section covers essential commands for managing users and groups.

**Important Note:** On many systems (including most Linux distributions), you'll need _root privileges_ to add, remove, or modify users and groups. This means you'll often need to use `sudo` before these commands. In a Docker container, you often _are_ the root user by default, but it's still best practice to be mindful of privileges.

---

### `passwd`

- **Description:** Changes a user's password.
- **Example Usage:**

  ```bash
  passwd        # Change your *own* password (no sudo needed)
  sudo passwd newuser  # Set or change the password for 'newuser' (requires root privileges)
  ```

  _Sample Output (when changing your own password):_

  ```
  Changing password for user.
  (current) UNIX password:  # You'll be prompted to enter your current password
  New password:             # Then, enter your new password (twice for confirmation)
  Retype new password:
  passwd: password updated successfully
  ```

  _Sample Output (setting a new password as root):_

  ```
  Enter new UNIX password:
  Retype new UNIX password:
  passwd: password updated successfully
  ```

---

### `adduser`

- **Description:** Creates a new user account. This command typically does the following:

  - Adds a new entry to `/etc/passwd` (user information).
  - Adds a new entry to `/etc/shadow` (secure password information).
  - Adds a new entry to `/etc/group` (if a primary group is created).
  - Creates a home directory for the new user (usually in `/home`).
  - Copies default files (e.g., `.bashrc`) to the new user's home directory.

- **Example Usage:**

  ```bash
  sudo adduser newuser  # Creates a new user named 'newuser' (requires root privileges)
  ```

  _Sample Output (truncated - it's interactive):_

  ```
    Adding user `newuser' ...
    Adding new group `newuser' (1001) ...
    Adding new user `newuser' (1001) with group `newuser' ...
    Creating home directory `/home/newuser' ...
    Copying files from `/etc/skel' ...
    New password:
    Retype new password:
    passwd: password updated successfully
    Changing the user information for newuser
    Enter the new value, or press ENTER for the default
      Full Name []: New User
      Room Number []:
      Work Phone []:
      Home Phone []:
      Other []:
    Is the information correct? [Y/n] y

  ```

  _Note:_ `adduser` is generally preferred over `useradd` on Debian/Ubuntu systems because `adduser` is a higher-level command that performs additional setup steps (like creating the home directory). `useradd` is a lower level command.

---

### `deluser`

- **Description:** Deletes a user account.
- **Example Usage:**

  ```bash
  sudo deluser newuser          # Removes the user 'newuser' (but keeps their home directory)
  sudo deluser --remove-home newuser  # Removes 'newuser' *and* their home directory
  sudo deluser --remove-all-files newuser # Removes all files owned by the user.
  ```

  _Sample Output (for `sudo deluser newuser`):_

  ```
  Removing user `newuser' ...
  Warning: group `newuser' has no more members.
  Done.
  ```

---

### `usermod`

- **Description:** Modifies an existing user account's properties (login name, home directory, group memberships, etc.).
- **Example Usage:**

  ```bash
  sudo usermod -l newlogin oldlogin   # Changes the login name from 'oldlogin' to 'newlogin'
  sudo usermod -d /new/home/dir -m newuser # Changes 'newuser's home directory to /new/home/dir and *moves* the contents
  sudo usermod -aG sudo newuser        # Adds 'newuser' to the 'sudo' group (giving them sudo privileges)
  sudo usermod -g newgroup user      # change the user's primary group.
  sudo usermod -L user     # lock the account by making the password invalid.
  ```

  _Key Options for `usermod`:_

  - `-l newlogin`: Changes the user's login name.
  - `-d /new/home/dir`: Changes the user's home directory.
  - `-m` (with `-d`): _Moves_ the contents of the old home directory to the new one. Important!
  - `-aG group1,group2,...`: Adds the user to the specified groups. `-a` (append) is _crucial_ here; without it, the user will be removed from all other groups!
  - `-g`: change user's primary group.
  -     `-L`: lock the user account.

---

### `su` (Switch User)

- **Description:** Switches to another user account _within the current terminal session_.
- **Example Usage:**

  ```bash
  su newuser       # Switch to the 'newuser' account (you'll be prompted for 'newuser's password)
  su - newuser    # Switch to 'newuser' and *also* load their environment (like their .bashrc) - highly recommended
  su               # Switch to the root user (you'll be prompted for the root password)
  su -             # Switch to the root user and load the root environment.
  exit             # Exit the switched-to user and return to your previous user.
  ```

  _Note:_ The `-` (dash) with `su` is extremely important. It makes the shell a _login shell_, which means it sources the user's profile scripts (like `.bashrc`). This ensures you have the correct environment for that user. Without the `-`, you might have unexpected behavior.

---

### Groups and Permissions

- **Groups:** Groups are collections of users. They are used to manage permissions on files and directories. For example, you might create a group called `developers` and give that group read/write access to a project directory.

- **Key Files:**

  - `/etc/passwd`: Contains user account information (username, user ID, home directory, etc.).
  - `/etc/shadow`: Contains _secure_ password information (hashed passwords).
  - `/etc/group`: Contains group information (group name, group ID, members).

- **Commands for Viewing Group Information:**

  ```bash
  cat /etc/group      # Display all groups on the system
  groups              # Show the groups the *current* user belongs to
  groups username     # Show the groups a specific user belongs to
  id                  # Show the current user's ID, primary group ID, and group memberships
  id username         # Show the user ID, primary group ID, and group memberships for a specific user
  ```

  _Sample Output:_

  ```
  uid=1000(user) gid=1000(user) groups=1000(user),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),116(lpadmin),126(sambashare)
  ```

- **Commands for Managing Group:**
  ```bash
    sudo groupadd newgroup  # Create a new group named 'newgroup'
    sudo groupdel groupname  # Delete a group
    sudo usermod -aG newgroup username # Adds the user to the group.
    sudo gpasswd -d user groupname # remove user from the group
  ```
