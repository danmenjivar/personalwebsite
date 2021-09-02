---
title: "Git Cheat Sheet"
date: 2020-07-14T09:29:31-07:00
toc: true
draft: true
---

## Terminology

| term            | definition                                                                                                                                                                                         |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Branch          | Another path, or line, of development in the repository.                                                                                                                                           |
| Check out       | To request a copy of a file so you can work on it; a typical feature of centralized version control systems.                                                                                       |
| Clone           | To make a copy of a repository that exists somewhere locally (in another directory) or remotely (on another server, or Git hosting site such as GitHub).                                           |
| Commit          | A change that’s saved to a repository, recording itself into the timeline.                                                                                                                         |
| Distributed     | A characteristic of a system such that its operations can be performed without the need of a server (as opposed to centralized).                                                                   |
| Repository      | A storage area for files; in the context of version control, this storage area is usually a directory or folder with special operations for viewing the timeline, committing files, and branching. |
| Staging area    | A feature of Git that enables the developer to commit certain parts of files instead of the whole file.                                                                                            |
| Timeline        | A set of events ordered by time, from the earliest to the most recent event; also known as a history                                                                                               |
| Version control | The practice of keeping track of changes such that you can always go back to a known state.                                                                                                        |

## Git Command Basics

| cmd                                      | description                                            |
| ---------------------------------------- | ------------------------------------------------------ |
| `git config --global user.name <name>`   | Add your name to the global Git configuration          |
| `git config --global user.email <email>` | Add your email address to the global Git configuration |
| git config --list                        | Display all the Git configurations                     |
| git config user.name                     | Display the user.name configuration value              |
| git config user.email                    | Display the user.email configuration value             |
| git help help                            | Ask Git for help about its help system                 |
| git help -a                              | Print all available Git commands                       |
| git --paginate help -a                   | Paginate the display of all Git commands               |
| git help -g                              | Print all available Git guides                         |
| git help glossary                        | Display the Git glossary                               |

## Making & Using a Git Repository

| cmd               | description                                                      |
| ----------------- | ---------------------------------------------------------------- |
| git init          | Initialize a Git repository in the current directory             |
| git status        | Display status of current directory, as it relates to Git        |
| git add FILE      | Start tracking FILE in Git; adds FILE to the staging area        |
| git commit -m MSG | Commit changes to the Git repository, with a message (in quotes) |
| git log           | Display the log (history) of the Git repository                  |
| git log --stat    | Display the log with the files that were modified                |
| git ls-files      | List the files in the repository                                 |

## Tracking & Updating Files

| cmd                           | description                                                                                 |
| ----------------------------- | ------------------------------------------------------------------------------------------- |
| git commit -m "Message"       | Commit changes with the log message entered on command line via the -m switch               |
| git diff                      | Show any changes between the tracked files in the current directory and the repository      |
| git commit -a -m "Message"    | Perform a git add, and then a git commit with the supplied log message                      |
| git diff --staged             | Show any changes between the staging area and the repository                                |
| git add --dry-run .           | Show what git add would do                                                                  |
| git add .                     | Add all new files in the current directory (use git status afterward to see what was added) |
| git log --shortstat --oneline | Show history using one line per commit, and listing each file changed per commit            |

## Committing Parts of Changes

| cmd                | description                                                                    |
| ------------------ | ------------------------------------------------------------------------------ |
| git rm file        | Remove file from staging area                                                  |
| git mv file1 file2 | Rename file1 to file2 in the staging area                                      |
| git add -p         | Pick parts of your changes to add to the staging area                          |
| git reset file     | Reset your staging area, removing any changes you’ve added with git add        |
| git checkout file  | Check out the latest committed version of the file into your working directory |

## Working with GitHub

| cmd                                                        | description                                                                                                      |
| ---------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| git remote add github https://github.com/yourname/math.git | Add a rename named github that points to your math repo on GitHub. (Replace yourname with your GitHub username.) |
| git push -u github master                                  | Push your master branch to the remote identified by GitHub, and set it to the upstream                           |
| git clone https://github.com/yourname/math.git             | Clone your GitHub repository named math. (Replace yourname with your GitHub username.)                           |

This Git cheat sheet was compiled from the chapters of _Learn Git in a Month of Lunches_ by Rick Umali.
