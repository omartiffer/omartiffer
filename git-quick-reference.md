
[:arrow_left Back to profile](./README.md)

---
# Git Commands Quick Reference

This document is a personal reference of Git commands I've learned and used, intended as a quick guide for common operations and useful tips and tools.

<br>

---
# Index

### 1. [Git Porcelain Commands](#git-porcelain-commands)
- [Basic](#basic)
- [Tracking changes](#tracking-changes)
- [Commit History](#commit-history)
- [Branching](#branching)
- [Merge, Rebase, Squash, and Cherry-picking](#merge-rebase-squash-and-cherry-picking)
- [Remotes](#remotes)
- [Configuration](#configuration)
- [Miscelaneous](#misc)
### 2. [Git Plumbing Commands](#git-plumbing-commands)
### 3. [Commit Message Best Practices](#commit-message-best-practices)
### 4. [Resources](#resources)

<br>

## Git Porcelain Commands

### Basic

`git init` - Initialize a folder as a repo.

`git status` - Check the current status of the working tree and staging area (any untracked, renamed, deleted, modified, or staged file).

`git status --short` - Show status in a compact format.

`git add` - Add changes on the working tree to the staging area.

`git commit -m "Commit message"` - Commit the staged changes to repo. 

[:arrow_up_small Back to top](#git-commands-quick-reference)

---

### Tracking changes

`git diff` - Show changes made to files in the working tree since last commit.

`git diff --staged` or `git diff --cached` - Show staged changes compared to the last commit.

`git diff HEAD` - Show all changes, staged and unstaged.

`git diff -w` - Ignore whitespace from diff.

`git diff <commit_hash>` - Show changes between the specified commit and current working tree.

`git diff <commit_hash_1>...<commit_hash_2>` - Show changes between commits (uses a common ancestor commit as starting point if the commits belong to different branches).

`git diff <branch_name_1>...<branch_name_2>` - Show changes between branches starting at a common ancestor commit.

`git show <diff_index_hash>` - Show original file being compared in diff.

[:arrow_up_small Back to top](#git-commands-quick-reference)

---

### Commit history

`git log` - Provide a view of the commit history.

`git log --oneline` - Show commit history (one line per commit).

`git log --graph` - Show a visual representation of the commit history

`git log --stat` - Provide additional info on what files were changed in each commit.

`git log --patch` - Provide additional info on the specific changes that were commited.

`git log <branch_name>` - Show commit history for the specified branch.

`git commit --amend` - Modify the latest commit in the history.

`git reset --soft <commit_hash>` - Reset HEAD to the specified commit without touching the staging area or working tree.

`git reset --mixed <commit_hash>` - Default behavior. Same as previous but only keeps the working tree.

`git reset --hard <commit_hash>` - Discard all commits from the specified commit up to the last commit.

`git reflog` - Show a history of where HEAD has been, effectively keeping track of all operations on the commit history. Can be used with `git reset` or `git cherry-pick` to "recover" a discarded commit.

[:arrow_up_small Back to top](#git-commands-quick-reference)

---

### Branching

`git branch -a` - List all branches in the local repo

`git branch <branch_name>` - Create a new branch.

`git branch -m <new_name>` - Rename the current branch to the new name.

`git branch -m <current_name> <new_name>` - Rename a branch.

`git branch -d <branch_name` - Delete a branch.

`git branch -D <branch_name>` - Force delete a branch (and all commits).

`git switch <branch_name>` - Move the HEAD to the specified branch (switch branches).

`git switch -c <branch_name>` - Create a new branch and immediately switch to it.

`git checkout <branch_name>` - Move the HEAD to the specified branch (switch branches).

`git checkout -b <branch_name>` - Create a new branch and immediately check out to it.

`git checkout <commit_hash>` - Move the HEAD to the specified commit (detached mode).

[:arrow_up_small Back to top](#git-commands-quick-reference)

---

### Merge, Rebase, Squash, and Cherry-picking

`git merge <branch_name>` - Merge all commits **FROM** the specified branch **TO** the current branch.

`git merge --abort` - Stop merge and return working tree to previous state (before merge started).

`git merge-base <branch1> <branch2>` - Determine the best common ancestor for a rebase.

`git rebase <branch_name>` - Rebase current branch commits **ON** the specified branch.

`git rebase <commit_hash>` - Rebase current branch commits **ON** the specified commit.

`git rebase -i <branch_name>|<commit_hash>` - Same as previous two, but interactive.

`git cherry-pick <commit_hash>` - Copy the specified commit and append it to the HEAD of current branch.

[:arrow_up_small Back to top](#git-commands-quick-reference)

---

### Remotes

`git clone <remote_url>` - Pull the remote repo from remote url.

`git remote add <name> <url>` - Track the main branch and HEAD of a hosted repo (remote).

`git remote -v` - Show URLs (fetch and push) for all remotes.

`git fetch` - "Download" changes in the remote branch to our local repo (needs merge as an adittional step to integrate changes/resolve conflicts).

`git push` - "Upload" local changes on current branch to the remote.

`git pull` - Download and merge (fetch + merge) changes in the remote branch in a single step.

`git ls-remote` - List all branches in remote.

`git branch -a` - List all branches (local and remote).

`git fetch origin <remote_branch>` - Fetches the remote branch to local (without creating a local branch, see next command).

`git checkout --track <remote_branch>` - Set up local branch to track remote branch (previously fetched).

[:arrow_up_small Back to top](#git-commands-quick-reference)

---

### Configuration

`git config --local|--global|--system <section>.<key> <value>` - Configure the specified key-value pair within the specified configuration section (user, core, etc.). `--local` is equivalent to the repo level, `--global` is equivalent to the OS user level, and `--system` is equivalent to the git installation level.

`git config --list` - Show all git configuration values.

`git config --list --show-origin` - Show all git configuration values and the file (level) where they are defined.

`git config <section>.<key>` - Show the value for the specified configuration section and key.

`git config --local|--global|--system --unset <section>.<key>` - Remove value for the especified key in the specified section at the specified level.

`git config --local|--global|--system --edit` - Edit configuration at the specified level (opens up the corresponding configuraion file in the default editor).

`git config --local|--global|--system --remove-section <section>` - Remove the specified section at the specified level.

[:arrow_up_small Back to top](#git-commands-quick-reference)

---

### Misc

`git stash` - Stash changes temporarily to clean the working tree.

`git stash pop` - Unstash previously stashed changes to the working tree.

`git tag <tag_name>` - Create a tag for the current commit in the current branch.

`git tag -a -m <tag_name> <message>` - Create an annotated tag for the current commit in the current branch.

[:arrow_up_small Back to top](#git-commands-quick-reference)

---

<br>

## Git Plumbing Commands

`git hash-object --stdin` - Generate a SHA1 hash for the text passed from STDIN and prints it to STDOUT.

`git hash-object -w --stdin` - Generate hash for the content passed from STDIN and saves it as a **blob** to the repo.

`git cat-file -t  <hash>` - Print the saved object's type for the provided hash.

`git cat-file -p <hash>` - Print the saved object's contents.

`git count-objects` - Count the number of objects in Git's object database.

`git show-ref <branch_name>` - List all tracked branches that have the specified branch name in their names.

[:arrow_up_small Back to top](#git-commands-quick-reference)

---

<br>

## Commit Message Best Practices

- **Use the imperative mood**: e.g., *Add feature*, *Fix bug*, *Refactor method*, instead of *Added* or *Adding*.
- **Keep the subject line under 50 characters**.
- **Capitalize the subject line**.
- **Do not end the subject line with a period**.
- **Use the body to explain *what* and *why*, not *how***.
- **Wrap the body at 72 characters** per line for readability.
- **Reference issues or tickets** when relevant.

Example:

```
Add error handling for API failures

Refactors the request handler to catch timeouts and HTTP 500 errors.
Logs all failures to Sentry for tracking. Related to #245.
```

[:arrow_up_small Back to top](#git-commands-quick-reference)

---

<br>

## Resources

1. [Git Docs](https://git-scm.com/doc) - Git's official documentation.
2. [Visualizing Git Tool](https://git-school.github.io/visualizing-git/) - An interactive tool to see how Git commands affect the commit graph. Illustrates what's going on underneath the hood when you use common Git operations. [Git School Repo](https://github.com/git-school/visualizing-git).
3. Resources on commit message best practices:
    - [Writing good commit messages](https://github.com/erlang/otp/wiki/writing-good-commit-messages)
    - [On commit messages](https://who-t.blogspot.com/2009/12/on-commit-messages.html)
    - [How To Write a Git Commit Message](https://cbea.ms/git-commit/)

[:arrow_up_small Back to top](#git-commands-quick-reference)
