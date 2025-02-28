---
title: Git Branching, Merging, and Conflicts
parent: Git & Version Control
nav_order: 66
layout: default
---

## Branching, Merging, and Conflicts

Branching and merging are fundamental concepts in Git that enable parallel development and collaboration. They allow you to isolate work on new features, bug fixes, or experiments without affecting the main codebase. This section covers creating, switching, pushing, and merging branches, as well as how to resolve merge conflicts.

---

## Branches

A branch represents an independent line of development. Think of it as a parallel version of your project. The default branch is usually `main` (or sometimes `master`). Branches allow you to work on different features or fixes concurrently without interfering with each other.

### Creating and Managing Branches Locally

- **`git branch` (List, Create, Delete)**

  - **Description:** Manages branches _locally_. Used to list existing branches, create new branches, and delete branches.
  - **Example Usage:**

    ```bash
    git branch           # List all *local* branches.  The current branch is marked with an asterisk (*).
    git branch my-new-feature  # Create a new branch named 'my-new-feature' (but don't switch to it).
    git branch -d my-old-feature # Delete the branch 'my-old-feature' (only if it's fully merged).
    git branch -D my-old-feature  # Force delete the branch 'my-old-feature' (even if it's not fully merged - BE CAREFUL!).
    git branch -a           # List all branches: local and remote-tracking branches.
    git branch -vv       # List local branches with verbose information, including the upstream branch (if set).
    git branch --merged    # List branches that have been merged into the current branch.
    git branch --no-merged # List branches that have *not* been merged into the current branch.
    ```

- **`git checkout` (Switch Branches / Create and Switch)**

  - **Description:** Traditionally used to switch between branches. This updates your working directory to match the state of the selected branch. It can _also_ create and switch to a new branch in one step.
  - **Example Usage:**

    ```bash
    git checkout main         # Switch to the 'main' branch.
    git checkout my-feature   # Switch to the 'my-feature' branch.
    git checkout -b my-new-feature  # Create a *new* branch named 'my-new-feature' AND switch to it (very common).
    ```

- **`git switch` (Switch Branches - Recommended)**

  - **Description:** A newer command (introduced in Git 2.23) specifically designed for switching branches. It's more focused and less overloaded than `git checkout`, making its purpose clearer and reducing the risk of accidental errors. Use `git switch` for switching branches, and `git checkout` for working with files (e.g., discarding changes).
  - **Example Usage:**

    ```bash
    git switch main       # Switch to the 'main' branch.
    git switch my-feature # Switch to the 'my-feature' branch.
    git switch -c my-new-feature  # Create a *new* branch named 'my-new-feature' AND switch to it. (-c is short for --create)
    ```

---

## Pushing a Branch to a Remote Repository

To share your branch with others (or create a backup), you need to push it to a remote repository (like GitHub, GitLab, or Bitbucket).

1.  **Make sure you're on the branch you want to push:**

    ```bash
    git switch your_branch_name
    ```

2.  **Commit any local changes.**

3.  **Push the branch:**

    ```bash
    git push -u origin your_branch_name  # The *first* time you push a new branch
    git push                      # On subsequent pushes (after setting the upstream with -u)
    ```

    _Explanation:_

    - `git push`: Uploads your local branch to the remote repository.
    - `-u origin your_branch_name`:
      - `-u` (or `--set-upstream`): Sets the "upstream" tracking branch for your local branch. This creates an association between your local branch and a branch on the remote repository (usually named `origin`). This simplifies future pushes and pulls. You only need to use `-u` the _first_ time you push a new branch.
      - `origin`: The name of the remote repository (by convention, `origin` is the default name for the primary remote).
      - `your_branch_name`: The name of your local branch.

    _After setting the upstream, you can simply use `git push` and `git pull` without specifying the remote and branch name._

---

## Merging a Branch

Merging combines the changes from one branch (the "source" branch) into another (the "target" branch). This is how you integrate the work done on a feature branch back into the main line of development.

1.  **Switch to the target branch (the branch you want to merge _into_):**

    ```bash
    git switch main  # Typically, you merge feature branches *into* 'main'
    ```

2.  **Ensure your target branch is up-to-date:**

    ```bash
    git pull origin main  # Get the latest changes from the remote 'main' branch
    ```

3.  **Merge the source branch:**

    ```bash
    git merge your_feature_branch  # Merge 'your_feature_branch' into the current branch (which should be 'main')
    ```

4.  **(If there are no conflicts):** Git will create a "merge commit" that combines the changes. Your editor will open to allow you to write a commit message (a default message is usually provided). Save and close the editor to complete the merge.

5.  **(If there are conflicts):** Git will tell you which files have conflicts. You'll need to _manually_ resolve these conflicts (see the "Merge Conflicts" section below).

6.  **Push the merged changes (if working with a remote):**

    ```bash
    git push origin main
    ```

7.  **Delete the feature branch (optional, but good practice):**

    ```bash
    git branch -d your_feature_branch   # Delete the local branch (safe if fully merged)
    git push origin --delete your_feature_branch  # Delete the remote branch
    ```

    Use `-d` to delete a branch _only if_ it has been fully merged. If Git detects unmerged changes, it will prevent the deletion. Use `-D` (uppercase) to _force_ deletion, even if the branch has unmerged changes (use with caution!).

---

## Merge Conflicts

A merge conflict occurs when Git cannot automatically merge changes because two branches have modified the same line(s) of the same file(s), or when one branch deletes a file that another branch modifies. Git needs your help to decide which changes to keep.

1.  **Identify Conflicting Files:** After a failed merge attempt (`git merge` or `git pull`), Git will output a message indicating which files have conflicts:

    ```
    Auto-merging file.txt
    CONFLICT (content): Merge conflict in file.txt
    Automatic merge failed; fix conflicts and then commit the result.
    ```

    You can also use `git status` to see a list of unmerged paths:

    ```bash
    git status
    # ...
    # Unmerged paths:
    #   (use "git add <file>..." to mark resolution)
    #
    #       both modified:   file.txt
    ```

2.  **Open the Conflicting File(s):** Open the conflicting file(s) in your text editor. Git has added special markers to show the conflicting sections:

    ```
    <<<<<<< HEAD
    This is the content from the current branch (e.g., main).
    =======
    This is the content from the branch you're merging in (e.g., feature_branch).
    >>>>>>> feature_branch
    ```

    _Marker Explanation:_

    - `<<<<<<< HEAD`: Beginning of the changes from your current branch (`HEAD`).
    - `=======`: Separator between the changes from the two branches.
    - `>>>>>>> feature_branch`: End of the changes from the other branch (the branch name or commit hash will be shown).

3.  **Resolve the Conflict:** Edit the file to decide how to combine the changes. You have several options:

    - **Keep your changes (HEAD):** Delete the lines from the other branch and _all_ the conflict markers.
    - **Keep the other branch's changes:** Delete the lines from your current branch (`HEAD`) and _all_ the conflict markers.
    - **Combine the changes:** Edit the file to create a new, merged version that incorporates parts of both versions. _Remove all conflict markers._
    - **Rewrite the section:** If neither version is suitable, rewrite the entire section. _Remove all conflict markers._

    _After resolving the conflict, the file should look like normal code, with no Git conflict markers._

4.  **Stage the Resolved File(s):** After resolving conflicts in a file, stage it using `git add`:

    ```bash
    git add file.txt  # Stage the resolved 'file.txt'
    git add .       # Stage *all* resolved files
    ```

5.  **Commit the Resolution:** Create a commit to finalize the merge. This commit records how you resolved the conflicts.

    ```bash
    git commit  # Opens your editor to create a commit message
    ```

    Or, for a one-line message:

    ```bash
    git commit -m "Resolved merge conflict in file.txt"
    ```

    It is not necessary to add the file name to the commit message, but it can improve readability.

6.  **Push (If Applicable):** If working with a remote repository, `push` your changes after resolving conflicts and committing.

    ```bash
    git push origin main
    ```

---

## Merge Conflict Tools and Strategies

- **Visual Merge Tools:** For complex conflicts, visual merge tools can be invaluable. They offer a graphical interface to compare conflicting versions and select changes.

  - **meld** (cross-platform, open-source)
  - **Beyond Compare** (commercial, cross-platform)
  - **KDiff3** (cross-platform, open-source)
  - **Visual Studio Code** (built-in merge conflict resolution)
  - **IntelliJ IDEA / PyCharm / WebStorm** (built-in)
  - ...and many others

  Configure Git to use your merge tool:

  ```bash
  git config --global merge.tool meld # Example using meld
  git mergetool                     # Open the configured merge tool
  ```

- **`git merge --abort`:** If you get stuck or make a mistake during conflict resolution, you can _abort_ the merge with `git merge --abort`. This returns your working directory and index to the state they were in _before_ you started the merge. It's a safe way to "undo" a problematic merge.

- **`git checkout --ours` / `git checkout --theirs` (Use with CAUTION):** These commands provide a shortcut for accepting _either_ your version (`--ours`) or the other branch's version (`--theirs`) of an _entire file_ during a conflict.

  - `git checkout --ours path/to/file.txt`: Keep _your_ version of `file.txt`.
  - `git checkout --theirs path/to/file.txt`: Keep the _other_ branch's version.

  Use these commands _only_ when you're absolutely sure you want to completely discard one version of the file. They are _not_ suitable for combining changes.

- **Communication:** If working on a team, _communicate_ with the other developer(s) involved to understand their changes and agree on the best resolution.
- **Testing:** _Always_ thoroughly test your code after resolving merge conflicts to ensure that the merged code works correctly and that no bugs were introduced.

---
