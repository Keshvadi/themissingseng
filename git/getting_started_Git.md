---
title: Getting Started in Git
parent: Git & Version Control
nav_order: 63
layout: default
---

## Installation

Make sure you have Git installed

```bash
sudo apt install git
```

Verify with

```bash
git --version
```

You should see an output like:

```bash
git version 2.43.0
```

If not then you can install it with

### **Windows**

- Download [Git Installer](https://git-scm.com/downloads/win) and run it with the default settings

- Open the git bash and verify the installation with

```bash
git --version
```

### **Mac**

- install with HomeBrew

```bash
brew install git
```

- or with Xcode Command line tools

```bash
xcode-select --install
```

### **Linux**

- Ubuntu/Debian based

```bash
sudo apt update && sudo apt install git
```

---

## Setup Git

Once Git is installed, you are gonna want to configure git properly...

1. Set up your user information
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your-email@example.com"
   ```
2. Verify your configuration

   ```bash
   git config --global --list
   ```

   **_Note_**: You should see something like...

   ```bash
   user.name=Your Name
   user.email=your-email@example.com
   ```

3. See the Github tab to link your profile to your git repository.

- After connecting your account, test your connection with
  ```bash
  ssh -T git@github.com
  ```
  **_Note_**: You will see...
  ```bash
  Hi <your-username>! You've successfully authenticated.
  ```

---

## Create a Repository

1. **Create a new repo**
   ```bash
   git init --initial-branch=main
   ```
2. **Write a simple "Hello World" program**

   ```bash
   #include <iostream>
   int main()
   {
       std::cout << "Hello World!" << std::endl;
       return 0;
   }
   ```

3. **Compile it**

   ```bash
   g++ hello.cpp
   ```

4. **Make sure it runs**

   ```bash
   ./a.out
   ```

   Then see what has changed in the repo with this command

   ```bash
   git status
   ```

5. **Now stage the source code**

   ```bash
   git add hello.cpp
   ```

6. **Commit the changes**

   ```bash
   # -m adds a commit message, make sure it is informative!
   git commit -m "Initial Commit"
   ```

7. **Create a git ignore file**

   ```bash
   echo "a.out" > .gitignore
   ```

8. **To view the history of the repo**

   ```bash
   git log
   ```

   Shows who made what changes and when

**_Note:_** you can visit the GitHub to see how to work with Remote repositories.
