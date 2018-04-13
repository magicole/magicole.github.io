---
layout: single
title: Git Cheat Sheet
excerpt: Useful/common Git commands
categories: [programming]
---

This page will contain basic and/or useful git commands.

# General

## Status
This command gives you all of the basic information you need to know.

```bash
git status
```

## Clone over https

General way to clone into a folder. <repo_folder> is optional, git will default to creating a folder with the name of the repository.

```bash
git clone https://github.com/<username>/<repo>.git <repo_folder>
```

## Clone over ssh

Useful if you want to use keys with github so you don't have to type in your username/password everytime you push. Again, <repo_folder> is optional.

```bash
git clone ssh@github.com:<username>/<repo>.git <repo_folder>
```

## Pulling/Fetching
Pulling grabs commits from github and changes the necessary files on you local system. Fetching just grabs the proposed changes so you can review them.

```bash
git pull
git fetch
```

## Committing 
The process for committing is as follows: add the file changes to a commit then commit the file changes with a message.

```bash
git add <file1> <file2> <etc>
git commit -m 'commit message goes here'
```

## Pushing

To put your commits on github, you need to push them to the 'cloud'. Use either of the commands below. The second one is more specific/safe and should especially be used if you created a new local branch that you want to push up.

```bash
git push
git push origin <branch_name>
```

## Branching

List available local branches

```bash
git branch
```

List all brances, local and remote.

```bash
git branch -a
```

Create a new local branch. The second one bases <new_branch> off of <old_branch>.

```bash
git checkout -b <branch_name>
git checkout -b <new_branch> <old_branch>
```

Change to \<branch>.

```bash
git checkout <branch>
```

## Remote Info

Get info about the upstream remote

```bash
git remote show origin
```

# Submodules

Information about submodules is stored in ```.gitmodules``` in the root of your git repo.

## Init submodules from clone
```bash
git clone --recursive <repo_url>
```

or

```bash
git clone <repo_url>
git submodule init
git submodule update
```

## Add a submodule 

<repo_location> is optional.

```bash
git add submodule <git_repo_url> <repo_location>
```
