+++
title = 'Basic Git Commands'
date = 2025-10-19T10:48:23+08:00
draft = true
+++

This article will cover what Git is and the explanation of some Git commands that I usually use in my daily workflow.

<!--more-->

## What is Git?

Git is a **Version Control System (VCS)** that helps developers track changes in their codebase over time. It allows you to:

- Revert to previous versions  
- See who made which change  
- Manage multiple versions of a project simultaneously  

Git is very useful when we working on a team. It lets several developers work on the same project without overwriting each other’s changes.

---

## Essential Git Commands

Here is a breakdown of the basic Git commands that form the backbone of my workflow, from setting up a project to managing changes.

### 1. Initializing and Tracking Changes

Before you can use most Git commands, you need to create a Git repository and tell Git which files to track.

- **`git init`**: This command is the first step. It creates a new, empty Git repository in the current directory.
- **`git status`**: This command shows your current branch, modified files, staged files, and untracked files. You’ll use this one *a lot*.
- **`git add <file>`** / **`git add .`**: Stages changes for your next commit. The dot (`.`) stages *all* modified files at once.
- **`git commit -m "Your descriptive message"`**: This takes the changes you've staged with `git add` and permanently records them in the repository's history as a **commit**. The `m` flag lets you quickly write a short, descriptive message about the changes you made.
  Use clear, descriptive messages (see [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/#specification) for inspiration).

### 2. Branching and Switching Contexts

Branches are one of Git’s superpowers. They let you work on new features or fixes in isolation.

- **`git checkout <branch-name>`**: This is used to switch from one branch to another. It moves your **HEAD** (the pointer to your current working commit) to the specified branch, changing all the files in your working directory to match the state of that branch.
- **`git checkout -b <new-branch-name>`**: Creates a new branch and switches to it immediately. This is the usual way to start working on a new feature or bug fix.
  Some projects have different branch naming convention. You might want to see [Conventional Branch Naming](https://conventional-branch.github.io/) for inspiration.

### 3. Sharing and Syncing Work

These commands are crucial for collaborating with others via a remote repository (like GitHub, GitLab, or Bitbucket).

- **`git push`**: Uploads your local branch commits to the remote repository. This makes your changes available to others.
- **`git pull`**: Fetches and merges the latest changes from the remote branch into your current branch.  
  (It’s basically `git fetch` + `git merge`.)

### 4. Combining and Cleaning History

Once work is complete on a separate branch, you'll need to integrate those changes back into the main line of development.

- **`git merge <branch-to-merge>`**: This command is used to integrate changes from one branch into your current branch. It creates a **new commit** (a "merge commit") that joins the histories of the two branches.
- **`git rebase <target-branch>`**: Like `merge`, `rebase` integrates changes, but it does so by moving or "replaying" your commits onto the tip of another branch. This results in a cleaner, linear history by avoiding the extra merge commits.
  ⚠️ **Tip:** Avoid rebasing branches that others are already using. It can cause conflicts.  
  My personal rule is: *don’t rebase if the branch has already been pushed*.

### 5. Handling Work in Progress

Sometimes you need to pause your unfinished work without committing it. For example, to quickly switch to a different branch to fix an urgent bug.

- **`git stash`**: I just learn this command and I really love it. Basically, this command temporarily saves your local changes and reverts your working directory to the last commit.  
  Think of it as putting your work in a locker.  
  - Add the `-u` flag to include untracked files.  
  - Add a message for clarity: `git stash push -m "WIP: feature X"`.
- **`git stash list`**: This command shows you every stash that you have, including its messages if any.
- **`git stash pop`**: This command reapplies the most recent stash *and removes it* from the list.  
  If you want to keep the stash for later, use `git stash apply` instead

---

## Cheat Sheet

Here’s a quick reference table for the commands covered above:

| Command                        | Description                                  |
| ------------------------------ | -------------------------------------------- |
| `git init`                     | Create a new Git repository                  |
| `git status`                   | Show the current state of the repository     |
| `git add <file>`               | Stage specific files for commit              |
| `git add .`                    | Stage all modified files                     |
| `git commit -m "message"`      | Save staged changes as a commit              |
| `git checkout <branch>`        | Switch to another branch                     |
| `git checkout -b <new-branch>` | Create and switch to a new branch            |
| `git push`                     | Upload local commits to a remote repository  |
| `git pull`                     | Fetch and merge updates from a remote branch |
| `git merge <branch>`           | Combine another branch into your current one |
| `git rebase <branch>`          | Reapply your commits onto another branch     |
| `git stash`                    | Temporarily save your changes                |
| `git stash list`               | Show saved stashes                           |
| `git stash pop`                | Reapply and remove the most recent stash     |

---

## What Next?

Once you’re comfortable with these commands above, you can explore:

- `git log` for viewing commit history  
- `git revert` for undoing changes safely  
- GUI tools like **GitHub Desktop** or **VS Code’s Source Control**  

Git may seem intimidating at first, but once you get the hang of it, it becomes one of the most powerful tools in your developer toolkit.
