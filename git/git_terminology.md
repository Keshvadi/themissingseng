---
title: Git Terminology
parent: Git & Version Control
nav_order: 61
layout: default
---

## Git Terminology

Understanding Git terminology is crucial for effectively using Git. Here's a breakdown of key terms:

### Core Concepts

- **Repository (Repo):** A directory containing your project and _all_ of its version history. Git stores this history in a hidden `.git` folder inside the repository. Think of the repository as the entire project, including its past, present, and future.
- **Working Directory/Working Tree:** The directory on your computer where you directly edit files. This is where you make changes before adding them to Git's tracking.
- **Staging Area (Index):** A "draft space" where you prepare changes before committing them. You selectively add changes from your working directory to the staging area, and then commit _only_ those staged changes. This gives you fine-grained control over what goes into each commit.
- **Commit:** A snapshot of your project at a specific point in time. Each commit has a unique ID (a SHA-1 hash), a message describing the changes, an author, and a timestamp. Commits are the fundamental building blocks of Git's history.
- **Branch:** A named, independent line of development. The default branch is usually called `main` (or sometimes `master`). Branches allow you to work on new features, bug fixes, or experiments without affecting the main codebase. Think of branches as parallel universes for your project.
- **Merge:** The process of combining changes from one branch into another (e.g., merging a feature branch into the `main` branch).
- **HEAD:** A pointer to the currently checked-out commit or branch. It represents your current working state.

### Remote Repositories and Collaboration

<<<<<<< HEAD

### Rebase

- Rebasing in Git takes _your_ changes and reapplies them on top of the latest version of the branch, like stacking fresh edits on a new copy. This keeps the history clean instead of mixing old and new changes together.

### Remote Repository

- # A version of your repository stored on another server, like GitHub or GitLab. This allows you to share your work and collaborate. (The GitHub Section outlines this further)

* **Remote Repository:** A version of your repository hosted on a server (like GitHub, GitLab, Bitbucket, or a private server). Remotes allow you to collaborate with others and back up your work.
* **Clone:** Creating a _local_ copy of a _remote_ repository. This downloads the entire project history to your computer.
* **Push:** Uploading your local commits to a remote repository. This shares your changes with others.
* **Pull:** Downloading changes from a remote repository to your local repository _and_ merging them into your current branch. This keeps your local copy up-to-date with the remote.
* **Fetch:** Downloading changes from a remote repository to your local repository, _without_ merging them into your current branch. This allows you to see what's changed on the remote before integrating those changes.
  > > > > > > > 5eb2d5e (updated content)

### Other Important Terms

- **Conflict:** Occurs when two different branches have made changes to the same part of the same file. Git cannot automatically merge these changes; you must manually resolve the conflict by choosing which changes to keep (or creating a new, combined version).
- **`.gitignore`:** A file that tells Git which files or directories to _ignore_. You typically use this to exclude build artifacts, temporary files, and sensitive information (like API keys) from being tracked by Git.
- **Tag:** A specific point in Git history, typically used to mark release versions (e.g., v1.0.0, v1.1.0). Tags are like permanent labels on commits.
- **Fork:** A _copy_ of a repository (usually on a remote like GitHub). Forks allow you to experiment with changes without affecting the original project. You can then propose changes from your fork back to the original repository using a pull request.

---

## Git Structure and Workflow

Git's workflow revolves around these four areas:

1.  **Working Directory:** Your local files, where you make changes.
2.  **Staging Area (Index):** A "preview" area where you select the changes you want to include in your next commit.
3.  **Local Repository:** The `.git` directory inside your project, where Git stores all the commits (snapshots) and other metadata.
4.  **Remote Repository (Optional, but crucial for collaboration):** A copy of the repository hosted on a server (e.g., GitHub, GitLab).

**Typical Workflow:**

1.  **Make Changes:** Modify files in your working directory.
2.  **Stage Changes:** Use `git add` to add specific files or changes to the staging area.
3.  **Commit Changes:** Use `git commit` to create a snapshot of the staged changes, along with a descriptive message. This saves the snapshot in your local repository.
4.  **Push Changes (if collaborating):** Use `git push` to upload your local commits to a remote repository.
5.  **Pull Changes (if collaborating):** Use `git pull` to download changes from the remote repository and merge them into your local branch.
6.  **Create a Branch:** Use `git branch <branch_name>` to create a new branch.
7.  **Switch to a Branch:** Use `git checkout <branch_name>` or `git switch <branch_name>` (a newer, more user-friendly command) to switch to a different branch.
8.  **Merge a branch**: Use `git merge <branch_name>` to merge changes from the specified branch into your current branch.

This workflow allows for organized, tracked, and collaborative development. The staging area provides a crucial step for carefully reviewing and selecting changes before committing them. Branching enables parallel development without interference, and remote repositories facilitate collaboration and backup.

You can look at this [Git Merge Conflicts](https://www.atlassian.com/git/tutorials/using-branches/merge-conflicts) tutorial to see how to handle merge conflicts.

---
