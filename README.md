# Git and GitHub Workshop

## git

git is a version control software.
It allows you to take snapshots (called commits) of your project, so you can easily track the changes made to a project.
It works by storing the _difference_ between each commit (hence why your git repository typically doesn't grow too enormous).
That said, it works best for plain text files, and not so great for larger compressed files.
git also allows _branching_ - allowing you to make changes to a separate version of the project while leaving the working version untouched. When you're happy with the new changes, you can 'merge' them back into the main branch.
git also allows you to copy/synchronise code between computers with the concept of local of 'remote' version of the repository.
Note: git is separate to github - github is a website where you can host git repositories.
Some tutorials available:

* git tutorial from GitHub: <https://docs.github.com/en/get-started/getting-started-with-git>
  * Also others, e.g.:
  * <https://www.atlassian.com/git>
  * <https://www.atlassian.com/git/tutorials>
  * <https://git-scm.com/book/en/v2> -- an open-source book - very complete
  * <https://learngitbranching.js.org/> -- a nice interactive tutorial
* To set up ssh keys for github: <https://docs.github.com/en/authentication/connecting-to-github-with-ssh>

Link to the workshop slides: <https://docs.google.com/presentation/d/1_vr6rSFEnR3vQKaKaPAe4Y9ECy6QbMDHU4nevcCBGus/edit?usp=sharing>

## Getting started

* Install:
  * `sudo apt install git`    (ubuntu)
  * `brew install git`        (mac)
  * <https://git-scm.com/downloads> (windows)
    * The windows git comes with `git bash' (a basic shell) that will allow you to use command line commands
* Highly recommend using with Visual Studio Code: <https://code.visualstudio.com/>
  * Completely free and widely used; many useful plugins for coding/git/github etc.
  * Note: Visual Studio Code (vscode) is _not_ the same as ``Visual Studio'' (microsoft is great at naming things)
  * Other editors probably also fine, but why not lean in to the monopoly
* If you use windows for coding, I highly recommend you checkout WSL (windows subsystem for linux)
  * <https://learn.microsoft.com/en-us/windows/wsl/install>
  * Gives a linux terminal directly in windows (not a virtual machine)
  * Integrates really well with vscode (use the 'remote wsl') plugin
  * Then, just use the linux version of git be happy

## Basic "cheat sheet" (command line commands)

The following can be thought of as a quick 'cheat sheet' to help you remember the required commands.

### Basics

* `git init`: creates a new git repository, with data stored in the (hidden) '.git' directory
  * Don't edit anything in the .git directory
  * Don't put a git repo inside a dropbox/oneDrive etc. folder: they do not play nicely with each other
* `git status`: tells you what’s going on - current status of the repo
* `git add <filename>`: adds specific file to the staging area
  * `git add .`: adds all files to staging area (except those ignored by .gitignore)
  * a '.gitignore' file is a textfile that tells git which files should be tracked and/or ignored (see example)
* `git commit`: creates a new commit
  * This will automatically open a text editor app (usually vim) - you can change the default text editor in the settings
  * type ":q!" to exit vim without saving any changes, or ":x" to exit with saving changes
* `git commit -m "Commit message"`: creates a new commit with 'message'
* `git commit -a`: creates a new commit for all available files (careful!)
  * will only commit files that are already being tracked. Use `git add .` first to also add any new files
  * Will open whichever text editor git has set up as default for you to enter a commit message. You can change the default editor, e.g.:
    * `git config --global core.editor "gedit"` to use gedit
    * `git config --global core.editor "code"` to use vscode
    * `git config --global core.editor "vim"` to use vim
* `git commit -a -m "Commit message"`: adds all changed files and creates a new commit, with 'message'
* `git checkout <revision>`: updates HEAD and current branch
  * revision can be a name (branch name), or the hash of a specific commit
  * See below for branching

* `git log`: shows a flattened log of history
  * `git log --graph --pretty --oneline`: Nice way to visualise history as a graph (without 'oneline' to get full details)
* `git diff <filename>`: show changes you made relative to the staging area
* `git diff <revision> <filename>`: shows differences in a file between snapshots

* You may have to set your name and email when making your first commit (commits must track WHO made the commit):
  * Set your username: `git config --global user.name "FIRST_NAME LAST_NAME"`
  * Set your email address: `git config --global user.email "MY_NAME@example.com"`
  * If you use same email as your github profile, best results

### FAQ

* Why do I need to "stage" and then "add" - why isn't this one step
  * While it is common to want to commit _all_ the changes you have made in one go, it's also common for us _not_ to want to do this. Having a two-step process allows us to commit some of the changes we have made, without committing others. (You can even selectively commit only part of a file)
  * If you want to do both in one step, you may use `git commit -a -m "Commit message"`

### Branching and merging

* `git branch`: shows branches
* `git branch <name>`: creates a branch
* `git checkout -b <name>`: creates a branch and switches to it
  * (same as `git branch <name>` followed by `git checkout <name>`)
* `git merge <revision>`: merges 'revision' (may be a branch, or a commit hash) into current branch

### Remotes (push, pull)

* `git clone <remote-url>`: download repository from remote
* `git remote`: list remotes
* `git remote add <name> <url>`: add a remote (default remote name is 'origin')
* `git push <remote> <branchName>`: send objects to remote, and update remote reference (default remote name is 'origin')
  * e.g.: `git push origin main` pushes to remote version of 'main'
* `git fetch`: retrieve objects/references from a remote (without downloading the actual files)
* `git pull`: Pulls changes from remote branch into yours

### Forking and cloning

* You can 'clone' a reposity: download a git repo from a remote
  * `git clone <repo> <directory>`: 'repo' is the address of the reposity, directory is the name for the folder that will appear on you pc. Leave directory blank, and the folder will have the name of the git repo
  * e.g., `git clone https://github.com/benroberts999/git-workshop.git`
  * You will now have a copy of the entire git repo: commits and all. You can make new edits and commits
    * If you want to push your changes up to the existing remote, you either need permissions or to do a pull request via github
* Forking is similar to cloning, except the repo is copied directly on github.com; you can then clone your copy of the reop

### Undo commits (keep changes to files)

* `git commit --amend`: edit a commit’s contents/message (careful!)
  * This should essentially never be done if a commit has already been pushed to the remote
* `git reset HEAD <file>`: unstage a file
* `git reset HEAD~1` : undoes last 1 commit (keeps file changes)

### Undo commits and changes **CAREFUL**

* `git checkout -- <file>`: discard all changes to file <file>
  * **careful**: cannot be undone
* `git reset --hard` : discards all changes since last commit
  * **careful**: cannot be undone

## gitignore

Typically, we don't want git to track _all_ the files in our repository.
For example, we typically want to track source files, but not compiled executables.
We also often don't want to track produced images, plots, large output files etc.
A '.gitignore' file is a (hidden) plain text file that tells git to ignore certain files (i.e., to not track them).
This is not required, but is usually a good idea.

* List file patterns in ".gitignore" (with the '.' in filename) that you don't want git to track
* lines beginning with '!' means 'except'.
  * I like to tell it to ignore everything (use "*"),
  * except for certain files (example: "!*.cpp")

It's common to take one of two approaches:

  1. list specific files for git to ignore
  2. Tell git to ignore everything, then list specific file patterns to allow

### Example .gitignore file

Here, I'll give three common examples.

 **1.** Ignore specific files:

For example:

```txt
*.log
*.aux
*.out
*.synctex.gz
```

* Ignores all .log, .aux, ..etc. files

**2.(a)** Ignore everything, except (basic):

```txt
*
!src/
!/src/*.cpp
!/src/*.hpp
!*.md
!.gitignore
```

* Ignores all files
* Except for the /src/ directory
* and any cpp/hpp files in the /src/ directory
* and any .md (markdown) files
* and the .gitignore file

**2.(b)** Ignore everything, except (advanced):

```txt
## ignore all files in all subdirectories (including /)
**/*

## except: all subdirectories (just folders)
!**/

## except: gitignore file (only the one in /)
!.gitignore

## except: any file in any subdirectory that matches:
!**/*.md
!**/*.cpp
!**/*.hpp
!**/*.ipp
!**/*.sh
!**/*.txt
!**/*.gnu
!**/*.py
## ... continue to list any file-types you want git to track
```

* This tells git to ignore everything, except all files in all sub-directories that match the specific patterns.
* Requires at least version 1.8.2 of git (many years old at this stage, shouldn't be a problem)
