
[⬅️ Back to profile](https://github.com/omartiffer)

---
# Git Commands Quick Reference

This document is a personal reference of Git commands I've learned and used. It is intended as a quick guide for common operations and useful tips and tools.

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
- [Identifying bad code (bisect)](#identifying-bad-code-bisect)
- [Configuration](#configuration)
- [Submodules](#submodules)
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

[🔼 Back to top](#git-commands-quick-reference)

---

### Tracking changes

`git diff` - Show changes made to files in the working tree since the last commit.

`git diff --staged` or `git diff --cached` - Show staged changes compared to the last commit.

`git diff HEAD` - Show all changes, staged and unstaged.

`git diff -w` - Ignore whitespace from diff.

`git diff <commit_hash>` - Show changes between the specified commit and the current working tree.

`git diff <commit_hash_1>...<commit_hash_2>` - Show changes between commits (uses a common ancestor commit as a starting point if the commits belong to different branches).

`git diff <branch_name_1>...<branch_name_2>` - Show changes between branches starting at a common ancestor commit.

`git show <diff_index_hash>` - Show the original file being compared in diff.

[🔼 Back to top](#git-commands-quick-reference)

---

### Commit history

`git log` - Provide a view of the commit history.

`git log --oneline` - Show commit history (one line per commit).

`git log --graph` - Show a visual representation of the commit history

`git log --stat` - Provide additional info on what files were changed in each commit.

`git log --patch` - Provide additional info on the specific changes committed.

`git log <branch_name>` - Show commit history for the specified branch.

`git commit --amend` - Modify the latest commit in the history.

`git reset --soft <commit_hash>` - Reset HEAD to the specified commit without touching the staging area or working tree.

`git reset --mixed <commit_hash>` - Default behavior. Same as previous, but only keeps the working tree.

`git reset --hard <commit_hash>` - Discard all commits from the specified commit up to the last commit.

`git reflog` - Show a history of where HEAD has been, effectively keeping track of all operations on the commit history. It can be used with `git reset` or `git cherry-pick` to "recover" a discarded commit.

[🔼 Back to top](#git-commands-quick-reference)

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

[🔼 Back to top](#git-commands-quick-reference)

---

### Merge, Rebase, Squash, and Cherry-picking

`git merge <branch_name>` - Merge all commits **FROM** the specified branch **TO** the current branch.

`git merge --abort` - Stop merge and return the working tree to the previous state (before merge started).

`git merge-base <branch1> <branch2>` - Determine the best common ancestor for a rebase.

`git rebase <branch_name>` - Rebase current branch commits **ON** the specified branch.

`git rebase <commit_hash>` - Rebase current branch commits **ON** the specified commit.

`git rebase -i <branch_name>|<commit_hash>` - Same as previous two, but interactive.

`git cherry-pick <commit_hash>` - Copy the specified commit and append it to the HEAD of the current branch.

[🔼 Back to top](#git-commands-quick-reference)

---

### Remotes

`git clone <remote_url>` - Pull the remote repo from the remote URL.

`git remote add <name> <url>` - Track the main branch and HEAD of a hosted repo (remote).

`git remote -v` - Show URLs (fetch and push) for all remotes.

`git fetch` - "Download" changes in the remote branch to our local repo (needs merge as an adittional step to integrate changes/resolve conflicts).

`git push` - "Upload" local changes on the current branch to the remote.

`git pull` - Download and merge (fetch + merge) changes in the remote branch in a single step.

`git ls-remote` - List all branches in remote.

`git branch -a` - List all branches (local and remote).

`git fetch origin <remote_branch>` - Fetches the remote branch to local (without creating a local branch; see the following command).

`git checkout --track <remote_branch>` - Set up the local branch to track the remote branch (previously fetched).

[🔼 Back to top](#git-commands-quick-reference)

---

### Identifying bad code (bisect)

`git bisect start` - Start the bisect process.

`git bisect good <commit_hash` - Specify good commit (start commit for the bisect process).

`git bisect bad <commit_hash>` - Specify good commit (end commit for the bisect process).

`git bisect good` - Clasify a commit as good during the bisect process.

`git bisect bad` - Clasify a commit as bad during the bisect process.

`git bisect run <test_suit_command` - Automatically evaluate commits by leveraging our test suite to clasify commits as either good or bad. For example `git bisect run npm test`.

`git bisect reset` - End bisect process.

[🔼 Back to top](#git-commands-quick-reference)

---

### Configuration

`git config --local|--global|--system <section>.<key> <value>` - Configure the specified key-value pair within the specified configuration section (user, core, etc.). `--local` is equivalent to the repo level, `--global` is equivalent to the OS user level, and `--system` is equivalent to the git installation level.

`git config --list` - Show all git configuration values.

`git config --list --show-scope` - Show all git configuration values and the scope (level) where they are defined.

`git config --list --show-origin` - Show all git configuration values and the file where they are defined.

`git config <section>.<key>` - Show the value for the specified configuration section and key.

`git config --local|--global|--system --unset <section>.<key>` - Remove the value for the specified key in the specified section at the specified level.

`git config --local|--global|--system --remove-section <section_name>` - Remove the specified configuration section at the specified level.

`git config --local|--global|--system --edit` - Edit configuration at the specified level (opens up the corresponding configuraion file on the default editor).

`git config --local|--global|--system --remove-section <section>` - Remove the specified section at the specified level.

`git config --global status.submoduleSummary true` - Tell git to show submodule information when running `git status`.

`git config --global diff.submodule log` - Tell git to enable submodule summaries when running diffs.

`git config --global push.recurseSubmodules on-demand` - Automatically push any changes from submodules to the remote when pushing from the parent repo.

`git config --local core.hooksPath .<dir_name>` - Specify a different location within the repo for git to look for hooks (.git directory by default).

[🔼 Back to top](#git-commands-quick-reference)

---

### Submodules

`git submodule add <remote_url> <local_path>` - Add remote repo as a submodule under the specified local path (directory).

`git submodule init` - Use after cloning a repo that has submodules to integrate with the config of your local repo.

`git submodule update` - Use after init to grab the content of the reference for the specific commit of the submodules.

`git submodule deinit <local_path>` - Temporarily remove the submodule at the local path (directory). It can be initialized again.

To permanently remove a submodule, use the following sequence of commands:

```bash
git submodule deinit <local_path>
git rm <local_path>
git commit -m "Commit message"
```

`git clone --recursive <remote_url> <local_repo_name>` - Clone repo with all tree of submodules, initialize, and update them.

`git submodule foreach '<command>'` - Execute command for each submodule in the repo. For example `git submodule foreach 'cat .gitmodules'`.

`git submodule sync --recursive` - Sync for remote changes in submodules.

`git submodule update --init --recursive` - Init and update all submodules in the tree after syncing.

---

### Misc

`git stash` - Stash changes temporarily to clean the working tree.

`git stash pop` - Unstash previously stashed changes to the working tree.

`git tag <tag_name>` - Create a tag for the current commit in the current branch.

`git tag -a -m <tag_name> <message>` - Create an annotated tag for the current commit in the current branch.

[🔼 Back to top](#git-commands-quick-reference)

---

<br>

## Git Plumbing Commands

`git hash-object --stdin` - Generate a SHA1 hash for the text passed from STDIN and print it to STDOUT.

`git hash-object -w --stdin` - Generate hash for the content passed from STDIN and save it as a **blob** to the repo.

`git cat-file -t  <hash>` - Print the saved object's type for the provided hash.

`git cat-file -p <hash>` - Print the saved object's contents.

`git count-objects` - Count the number of objects in Git's object database.

`git show-ref <branch_name>` - List all tracked branches that have the specified branch name in their names.

[🔼 Back to top](#git-commands-quick-reference)

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

[🔼 Back to top](#git-commands-quick-reference)

---

<br>

## Resources

1. [Git Docs](https://git-scm.com/doc) - Git's official documentation.
2. [Visualizing Git Tool](https://git-school.github.io/visualizing-git/) - An interactive tool to see how Git commands affect the commit-graph. Illustrates what's happening underneath the hood when using common Git operations. [Git School Repo](https://github.com/git-school/visualizing-git).
3. Resources on commit message best practices:
    - [Writing good commit messages](https://github.com/erlang/otp/wiki/writing-good-commit-messages)
    - [On commit messages](https://who-t.blogspot.com/2009/12/on-commit-messages.html)
    - [How To Write a Git Commit Message](https://cbea.ms/git-commit/)

[🔼 Back to top](#git-commands-quick-reference)
