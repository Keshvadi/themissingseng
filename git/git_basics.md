---
title: Git Basics
parent: Git & Version Control
nav_order: 65
layout: default
---

## Git Basics (init, add, commit, status)

This section will give an overview of the available commands in Git, as well as where and why you would use them. (They will be in the order you would typically use them.)

### `init`

- Git init takes your repository and start tracking it, you can just run this command in your desired directory...
  ```bash
  git init
  ```
- This creates a .git folder making your directory a Git repo.

### `status`

- Status shows you any changes made to the directory. (New files or elements will be marked untracked)
  ```bash
  git status
  ```

### `add`

- Files that have been edited or added will show up in red with a, deleted, modified or untracked label. Add will take these files and add them to the staging area, from which you will commit them

  ```bash
  ## adds the specified file chosen
  git add file_name.txt

  ## adds all of the changed files
  git add .
  ```

### `commit`

- If you rememeber from the teminology section, the commit is a snapshot of the project at a certain point in time (a version). Commit take the updates from your staging area and uploads it to your repository.

  ```bash
  git commit -m "<Comment explaining your changes (Make sure its good!!)>"
  ```

- **Note:** if you want to see the history of your commits, you can do so with **log**...

  ```bash
  git log

  ## shows the actual changes made in the commit
  git log -p
  ```

---

## Remote Repositories (GitHub)

The most commonly used remote repository is GitHub. If you are doing any sort of developing, GitHub is an essential tool that everyone looks for and is going to be a must have skill in industry work. With that said here is what you need to know...

1. `clone`

- This is covered in depth in the GitHub tab, but for now this is all you need
  ```bash
  git clone https://github.com/user/repo.git
  ```

2. `push`

- This sends your local commits to the remote repo's branch that you choose. (explained in branching tab)
- **Warning:** this can cause a thing called merge conflicts (covered in the Resolving conflicts tab)
  ```bash
  ## pushing changes to the main branch
  git push origin main
  ```

3. `pull`

- This gets you the latest version stored in the remote repo
- **Warning:** this can cause merge conflicts if your local version differs

  ```bash
  git pull origin main
  ```

---

## Pull Request (PR) and Issues

- **Pull Requests** are used to suggest changes to a repository.
  1. Push your changes
  2. Go to GitHub --> Open a Pull Request
  3. Wait for an approval and then merge
- **Issues** are used to track bugs or feature requests
  1. Open a repo
  2. Navigate to the Issues tab
  3. Click New Issue, describe the problem, and submit.

---

## Ignoring files

The .gitignore file tells Git which files and folders to ignore, so they don’t get committed to the repository.

### `.gitignore`

1. Create a file named .gitignore in the root of your repo.
2. Add files or folders you want Git to ignore.
3. Save the file, and Git will automatically exclude those files from tracking.

- Example .gitignore file

  ```bash
  # Ignore compiled files
  *.o
  *.out
  *.class

  # Ignore system files
  .DS_Store
  Thumbs.db

  # Ignore logs and temp files
  *.log
  /tmp/

  # Ignore environment variables
  .env
  ```

**Note:** to check files being ignored...

```bash
git status --ignored
```
