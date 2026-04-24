# Git Commands Cheatsheet

This cheatsheet provides a quick reference for commonly used Git commands at AquaPower. For detailed explanations, refer to the [Git Style Guide](git_style_guide.md) and [Git Flow Workflow](git_flow.md).

## Configuration

*   **Set your user name:**
    ```bash
    git config --global user.name "Your Name"
    ```
*   **Set your user email:**
    ```bash
    git config --global user.email "your.email@example.com"
    ```
*   **List all configs:**
    ```bash
    git config --list
    ```
*   **Set default editor:**
    ```bash
    git config --global core.editor "vim" # or "code --wait" for VS Code
    ```

## Initializing a Repository

*   **Initialize a new Git repository:**
    ```bash
    git init
    ```
*   **Clone an existing repository:**
    ```bash
    git clone <repository-url>
    ```

## Staging & Committing

*   **Check status of your working directory:**
    ```bash
    git status
    ```
*   **Add all changes to the staging area:**
    ```bash
    git add .
    ```
*   **Add specific file(s) to the staging area:**
    ```bash
    git add <file1> <file2>
    ```
*   **Commit staged changes:**
    ```bash
    git commit -m "Your descriptive commit message"
    ```
*   **Commit with a longer message (opens editor):**
    ```bash
    git commit
    ```
*   **Amend the last commit (edit message/files):**
    ```bash
    git commit --amend
    ```

## Branching

*   **List all local branches:**
    ```bash
    git branch
    ```
*   **List all branches (local and remote):**
    ```bash
    git branch -a
    ```
*   **Create a new branch:**
    ```bash
    git branch <branch-name>
    ```
*   **Create a new branch and switch to it:**
    ```bash
    git checkout -b <branch-name>
    # Or for newer Git versions:
    git switch -c <branch-name>
    ```
*   **Switch to an existing branch:**
    ```bash
    git checkout <branch-name>
    # Or for newer Git versions:
    git switch <branch-name>
    ```
*   **Delete a local branch (only if merged):**
    ```bash
    git branch -d <branch-name>
    ```
*   **Force delete a local branch (even if unmerged):**
    ```bash
    git branch -D <branch-name>
    ```

## Merging & Rebasing

*   **Merge another branch into your current branch:**
    ```bash
    git merge <branch-to-merge>
    ```
*   **Rebase your current branch onto another branch:**
    ```bash
    git rebase <base-branch>
    ```
    *   *Caution: Avoid rebasing branches that have already been pushed to a remote and shared with others.*
*   **Abort a rebase in progress:**
    ```bash
    git rebase --abort
    ```
*   **Continue a rebase after resolving conflicts:**
    ```bash
    git rebase --continue
    ```

## Remote Operations

*   **Show your remote repositories:**
    ```bash
    git remote -v
    ```
*   **Add a remote repository:**
    ```bash
    git remote add origin <repository-url>
    ```
*   **Fetch changes from remote (don't merge):**
    ```bash
    git fetch origin
    ```
*   **Pull changes from remote (fetch + merge):**
    ```bash
    git pull origin <branch-name>
    ```
*   **Push changes to remote:**
    ```bash
    git push origin <branch-name>
    ```
*   **Push your current branch and set upstream:**
    ```bash
    git push -u origin <branch-name>
    ```
*   **Delete a remote branch:**
    ```bash
    git push origin --delete <branch-name>
    ```

## History & Inspection

*   **Show commit history (current branch):**
    ```bash
    git log
    ```
*   **Show a concise commit history:**
    ```bash
    git log --oneline --graph --decorate
    ```
*   **Show differences between working directory and staging area:**
    ```bash
    git diff
    ```
*   **Show differences between staging area and last commit:**
    ```bash
    git diff --staged
    ```
*   **Show differences between two commits/branches:**
    ```bash
    git diff <commit1> <commit2>
    git diff <branch1> <branch2>
    ```
*   **View a specific commit:**
    ```bash
    git show <commit-hash>
    ```

## Undoing Changes

*   **Unstage a file:**
    ```bash
    git reset HEAD <file-name>
    ```
*   **Discard changes in working directory for a file:**
    ```bash
    git restore <file-name>
    ```
*   **Discard all changes in working directory:**
    ```bash
    git restore .
    ```
*   **Revert a commit (creates a new commit that undoes changes):**
    ```bash
    git revert <commit-hash>
    ```
*   **Reset to a previous commit (rewrites history - use with caution):**
    ```bash
    git reset --hard <commit-hash>
    ```
    *   *Caution: Do not `git reset --hard` on commits that have been pushed and shared.*
*   **Stash current changes (save for later):**
    ```bash
    git stash
    ```
*   **Apply the most recent stash:**
    ```bash
    git stash pop
    ```
*   **List all stashes:**
    ```bash
    git stash list
    ```

## Tagging

*   **Create a lightweight tag:**
    ```bash
    git tag <tag-name>
    ```
*   **Create an annotated tag (recommended for releases):**
    ```bash
    git tag -a <tag-name> -m "Tag message"
    ```
*   **Push tags to remote:**
    ```bash
    git push origin --tags
    ```
