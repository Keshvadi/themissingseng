---
title: GitHub
parent: Git & Version Control
<<<<<<< HEAD
nav_order: 64
=======
nav_order: 62
>>>>>>> 5eb2d5e (updated content)
layout: default
---

## GitHub

GitHub is a web-based platform that provides hosting for Git repositories. It's much more than just a place to store code; it's a comprehensive platform for collaboration, version control, project management, and open-source development. Think of it as a "cloud service for Git" plus a social network for developers.

**Key Features of GitHub:**

- **Remote Repository Hosting:** Store your Git repositories securely in the cloud.
- **Collaboration Tools:** Work with others on projects, manage contributions, track issues, and discuss changes.
- **Issue Tracking:** Report bugs, request features, and manage tasks.
- **Pull Requests:** Propose changes to a project and have them reviewed by others before merging. This is a _core_ part of the GitHub workflow.
- **Code Review:** Discuss and review code changes within pull requests.
- **Project Management:** Use features like projects, milestones, and labels to organize and track work.
- **Wiki and Documentation:** Create documentation for your projects.
- **GitHub Pages:** Host static websites directly from your GitHub repositories.
- **GitHub Actions:** Automate workflows, including CI/CD pipelines.
- **Community and Open Source:** Discover, contribute to, and learn from millions of open-source projects.
- **Profile Page**: Having a profile page that shows your activity.

---

## Getting Started with GitHub

1.  **Create a GitHub Account:** Go to [https://github.com/](https://github.com/) and sign up for a free account.

2.  **Create a Repository:** Follow the "Hello World" tutorial on GitHub: [Hello World](https://docs.github.com/en/get-started/start-your-journey/hello-world). This will guide you through creating your first repository on GitHub (your _remote_ repository).

3.  **Link Your Local Repository to GitHub:**

    - If you _already_ have a local Git repository, you can link it to a newly created _empty_ GitHub repository using the `git remote add` command:

      ```bash
      git remote add origin [https://github.com/your_username/your_repository_name.git](https://github.com/your_username/your_repository_name.git)  # Replace with your username and repo name
      git remote -v  # Verify the remote URL
      ```

    - If you're starting a _new_ project, it's often easier to _clone_ the GitHub repository to your local machine (see the "Cloning" section below).

# <<<<<<< HEAD

    *Explanation:*

    *   `git remote add origin ...`:  Adds a "remote" named `origin` to your local repository.  `origin` is a conventional name for the primary remote repository (you can have multiple remotes).
    *   `https://github.com/your_username/your_repository_name.git`:  This is the URL of your GitHub repository (you can find this on the repository's page on GitHub).

> > > > > > > 5eb2d5e (updated content)

---

## Cloning a Repository

Cloning creates a local copy of a remote repository (on GitHub or elsewhere).

- **Methods:**

  - **HTTPS:**
    ```bash
    git clone [https://github.com/user/repo.git](https://github.com/user/repo.git)
    ```
    You will be prompted for your GitHub username and password (or personal access token) when you push changes.

<<<<<<< HEAD

1.  **Set up Git with your GitHub Account**
    ```bash
    git config --global user.name "Your Name"
    git config --global user.email "youremail@email.com"
    ```
2.  # **Generate SSH key (Recommended for security)**

        *   **SSH:** (Recommended)
            ```bash
            git clone git@github.com:user/repo.git
            ```
            This requires setting up an SSH key (see below). SSH is more secure and convenient than HTTPS for frequent interactions.

    > > > > > > > 5eb2d5e (updated content)

        *   **GitHub CLI:**
            ```bash
            gh repo clone user/repo
            ```
             Requires installing the GitHub CLI ([https://cli.github.com/](https://cli.github.com/)). This is a convenient way to interact with GitHub from the command line.

- **Recommendation:** Set up an SSH key for GitHub. This avoids repeatedly entering your username and password.

---

## Integrating Your GitHub Account with Your Local Git

To interact with GitHub repositories (push, pull) without repeatedly entering your credentials, you need to configure your local Git installation.

# <<<<<<< HEAD 3. **Check Credentials to see if they are correct**

1.  **Set Your Git Username and Email:**

    > > > > > > > 5eb2d5e (updated content)

        ```bash
        git config --global user.name "Your Name"
        git config --global user.email "[email address removed]"
        ```

<<<<<<< HEAD

# check remote repository

git remote -v

````

---

## Linking your local repo to GitHub
This section will guide you in the case that you have a local repository (project on your computer) and you want to save it to a remote repository (save it to the cloud).
1. **Initialize or navigate to your repo**
```bash
# Find your repository
cd /your_repo_path

# or initialize a new repo
git init
````

2. **Add the remote repository**

- Go to your github and create a new repo, click the green code button and copy the link...
  - **using HTTPS:**
  ```bash
  git remote add origin https://github.com/your-username/repository-name.git
  ```
  - **using SSH:**
  ```bash
  git remote add origin git@github.com:your-username/repository-name.git
  ```

3. **Verify the remote link**

   ```bash
   git remote -v
   ```

   You should see something along the lines of:

   ```bash
   origin  https://github.com/your-username/repository-name.git (fetch)
   origin  https://github.com/your-username/repository-name.git (push)
   ```

4. **Push your local files to the remote repository**
   - If you have files to push
   ```bash
   git add .
   git commit -m "Initial commit"
   git push -u origin main
   ```

### **_Note_**: If you are working with other people, _PLEASE AVOID CONFLICTS_...

1. **Get the latest updates from the remote repository**
   ```bash
   # Downloads changes without merging them to your local repo
   git fetch origin
   ```
2. **Merge or Rebase**
   If you are okay with your changes

   ```bash
   git merge origin/main

   # or rebase
   git rebase origin/main
   ```

3. **Or Pull (Fetch and Merge in one command)**

   - This will fetch and merge changes for you automatically.
   - If conflicts occur, Git will ask you to resolve them before completing the merge.

   ```bash
   git pull origin main
   ```

---

## Cloning Repositories

Say you need to collaborate with another developer. In this case you will clone their repo onto your system so that you can make your changes. This can be done by clicking the green `code` button, which will open a dropdown menu. You should see...

- **HTTPS:** the easiest and most common way to clone a repo, but it requires authentication to push changes.
  ```bash
  git clone https://github.com/user/repo.git
  ```
- **SSH:** uses a key that you set up to your account, this makes your life easier and lets you push without needing authentication. This method is faster and more secure than HTTPS.
  ```bash
  git clone git@github.com:user/repo.git
  ```
- **GitHub CLI:** you can clone quickly if you have GitHubCLI installed. This removes the need to manually enter a URL
  ```bash
  gh repo clone user/repo
  ```

**Recommendation:** Set up an SSH key for GitHub to make pushing and pulling projects easier, avoiding repeated authentication prompts. Since you're likely copying the clone URL from GitHub anyway, the GitHub CLI’s URL-free cloning isn’t a major advantage. SSH is your best bet for long-term convenience.

### **Steps to clone**

1. **Clone the Repo**

   - Via HTTPS:

   ```bash
   git clone https://github.com/your-username/repository-name.git
   ```

   - Via SSH:

   ```bash
   git clone git@github.com:your-username/repository-name.git
   ```

2. **Make your changes and check what files you modified**

   ```bash
   git status
   ```

3. **Check if your files have been tracked and then Commit and Push**

   ```bash
   git add <files you created>
   # or you can add all the modified files with 'add .'
   git add .

   #check your working area to make sure the files are tracked
   git status

   #push all your changes
   git commit -a -m "Created files X,Y,Z and changed A,B,C"

   # You would ideally be working on your own branch: Denoted as Your_Branch
   git push origin Your_Branch
   ```

4. **Validate your changes with**
   ```bash
   git log
   ```

---

## Unlinking a Remote Repository

In the event that you want to disconnect your local machine from a remote repository you can follow the steps below. This can be useful if you are done working on a project and you don't want to accidentally push some changes, or if you accidentally duplicated a repository that you don't need.

### **Remove the Remote Origin**

```bash
git remote remove origin
```

Verify the removal with

```bash
git remote -v
```

=======
_Important:_ Use the email address associated with your GitHub account. The `--global` flag sets these configurations for all your Git repositories. You can set them per-repository by omitting `--global`.

2.  **Generate an SSH Key (Recommended for Security and Convenience):**

    ```bash
    ssh-keygen -t ed25519 -C "[email address removed]"  # Use ed25519 for a more modern key type (recommended over RSA)
    ```

    - Follow the prompts:
      - Press Enter to accept the default file location (`~/.ssh/id_ed25519`).
      - Enter a strong passphrase (highly recommended).
    - This command creates two files:
      - `~/.ssh/id_ed25519`: Your _private_ key (keep this secret!).
      - `~/.ssh/id_ed25519.pub`: Your _public_ key (this is what you'll add to GitHub).

    ```bash
     # add SSH key to SSH Agent
     eval "$(ssh-agent -s)"
     ssh-add ~/.ssh/id_ed25519
    ```

3.  **Add Your Public Key to GitHub:**

    - Copy the contents of your _public_ key file:

      ```bash
      cat ~/.ssh/id_ed25519.pub  # Display the public key
      ```

    - Go to your GitHub account settings:
      1.  Click on your profile picture (top right).
      2.  Select "Settings."
      3.  In the left sidebar, click "SSH and GPG keys."
      4.  Click "New SSH key."
      5.  Give the key a descriptive title (e.g., "My Laptop").
      6.  Paste the contents of your _public_ key into the "Key" field.
      7.  Click "Add SSH key."

4.  **Verify Your Configuration:**

    ```bash
    git config --list          # List your Git configuration
    git remote -v             # List your configured remote repositories (should show the SSH URL if you're using SSH)
    ssh -T git@github.com     # Test your SSH connection to GitHub
    ```

    _Expected output for `ssh -T git@github.com`:_

    ```
    Hi username! You've successfully authenticated, but GitHub does not provide shell access.
    ```

---

> > > > > > > 5eb2d5e (updated content)
