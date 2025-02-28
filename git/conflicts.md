---
title: Resolving Merge Conflicts in Git
parent: Git & Version Control
nav_order: 67
layout: default
---

## Merge Conflicts

Merge conflicts happen when two branches have made changes to the _same line_ of the _same file_, or when one branch deletes a file that another branch modifies. Git cannot automatically determine which version is correct, so it requires _manual intervention_ to resolve the conflict. A merge conflict can also happen when you `pull` from a remote repository and there are changes.

---

## How to Resolve Merge Conflicts

1.  **Identify the Conflicts:**

    After attempting a merge (e.g., `git merge feature_branch`) or `git pull` that results in conflicts, Git will output a message like this:

    ```
    Auto-merging file.txt
    CONFLICT (content): Merge conflict in file.txt
    Automatic merge failed; fix conflicts and then commit the result.
    ```

    This tells you which files have conflicts (in this case, `file.txt`). You can also use `git status` to see a list of unmerged paths:

    ```bash
    git status
    # On branch main
    # You have unmerged paths.
    #   (fix conflicts and run "git commit")
    #   (use "git merge --abort" to abort the merge)
    #
    # Unmerged paths:
    #   (use "git add <file>..." to mark resolution)
    #
    #       both modified:   file.txt
    #
    ```

2.  **Open the Conflicting File(s):**

    Open the conflicting file(s) in your text editor. Git will have added conflict markers to indicate the conflicting sections:

    ```
    <<<<<<< HEAD
    This is the content from the current branch (e.g., main).
    =======
    This is the content from the branch you're merging in (e.g., feature_branch) or remote branch.
    >>>>>>> feature_branch
    ```

    _Explanation of Markers:_

    - `<<<<<<< HEAD`: Marks the beginning of the changes from your current branch (`HEAD`).
    - `=======`: Separates the changes from your current branch and the other branch.
    - `>>>>>>> feature_branch`: Marks the end of the changes from the other branch (the branch name or a commit hash will be shown).

3.  **Resolve the Conflict:**

    Inside each conflicting section, you need to decide how to combine the changes. You have several options:

    - **Keep Your Changes (HEAD):** Delete the lines from the other branch and the conflict markers, leaving only the lines from your current branch (`HEAD`).
    - **Keep Their Changes (Other Branch):** Delete the lines from your current branch (`HEAD`) and the conflict markers, leaving only the lines from the other branch.
    - **Combine the Changes:** Edit the file to create a new, merged version that incorporates changes from _both_ branches. This is the most common approach.
    - **Rewrite the Section:** If neither version is correct, rewrite the entire section.

    *Crucially, after making your choice, you must *remove the conflict markers* (`<<<<<<<`, `=======`, `>>>>>>>`).* The file should look like normal code, without any Git markers.

    _Example (keeping only your changes):_

    ```
    This is the content from the current branch (e.g., main).
    ```

    _Example (combining changes):_

    ```
    This is the content from the current branch (e.g., main).
    This is additional content from the feature branch.
    ```

4.  **Stage the Resolved File(s):**

    After you've resolved the conflicts in a file and removed all conflict markers, stage the file using `git add`:

    ```bash
    git add file.txt  # Stage the resolved 'file.txt'
    git add .       # Stage *all* resolved files
    ```

5.  **Commit the Resolution:**

    Create a commit to finalize the merge and record the conflict resolution. Git will usually pre-populate the commit message with information about the merge, but you can edit it.

    ```bash
    git commit  # Opens your editor to create the commit message (recommended)
    ```

    Or, for a one-line message:

    ```bash
    git commit -m "Resolved merge conflict in file.txt"
    ```

6.  **Push (If Applicable):**

    If you're working with a remote repository, push your changes:

    ```bash
    git push origin main  # Or the name of your branch
    ```

---

## Merge Conflict Tools and Strategies

- **Visual Merge Tools:** For complex conflicts, visual merge tools can be incredibly helpful. These tools provide a graphical interface for comparing the conflicting versions and selecting changes. Examples include:

  - **meld** (cross-platform, open-source)
  - **Beyond Compare** (commercial, cross-platform)
  - **KDiff3** (cross-platform, open-source)
  - **VS Code** (built-in merge conflict resolution)
  - **IntelliJ IDEA / PyCharm / WebStorm** (built-in)
  - ...and many others.

  You can configure Git to use your preferred merge tool with `git mergetool`. For example, to configure `meld`:

  ```bash
  git config --global merge.tool meld
  git mergetool  # Open the configured merge tool to resolve conflicts
  ```

- **`git merge --abort`:** If you get stuck during a merge and want to start over, you can _abort_ the merge using `git merge --abort`. This will return your working directory and index to the state they were in _before_ you started the merge.

- **`git checkout --ours` / `git checkout --theirs` (Use with Caution!)**

  - These commands offer a very fast, but potentially dangerous, shortcut during a merge conflict.
    _`git checkout --ours path/to/file.txt`: Accepts **our** version for the conflict.
    _`git checkout --theirs path/to/file.txt`: Accepts **their** version for the conflict.
  - Use these commands when there are lots of conflicts and you can confidently choose one version over the other.

- **Communication:** If you're working on a team, communicate with the other developer(s) involved in the conflict to understand their changes and agree on the best resolution.

- **Testing:** _Always_ thoroughly test your code after resolving merge conflicts to ensure that the merged code works as expected and that no bugs were introduced.

---
