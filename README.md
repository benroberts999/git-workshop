Some helpful tips for students in our group:


## git

git is a version control software.
It allows you to take snapshots (called commits) of your project, so you can easily track the changes made to a project.
It works by storing the _difference_ between each commit (hence why your git repository typically doesn't grow too enormous).
That said, it works best for plain text files, and not so great for larger compressed files.
git also allows branching - allowing you to make changes to a separate version of the project while leaving the working version untouched. When you're happy with the new changes, you can 'merge' them back into the main branch.
git also allows you to copy/synchronise code between computers with the concept of local of 'remote' version of the repository.
Note: git is separate to github - github is a website where you can host git repositories.
Some tutorials available:
 * https://git-scm.com/book/en/v2 -- an open-source book - very complete
 * https://learngitbranching.js.org/ -- a nice interactive tutorial
 * Also others, e.g.:
 * https://www.atlassian.com/git
 * https://www.atlassian.com/git/tutorials


## Getting started

  * Install:
     * `$ sudo apt install git`    (ubuntu)
     * `$ brew install git`        (mac)
  * Plugins are available for most code-focused text editors and IDEs (e.g, Atom, Visual Studio code, etc.) - including on windows
  * There are also GUI versions (e.g., github desktop, which runs on all platforms and can be downloaded from the web). But these are often tricky to use for anything but the simplest of tasks. If you prefer to use a GUI, it's generally better to use a plugin for your IDE/editor
  * Use: `$ git help <command>` to get help (man page) for a specific git command

The following can be thought of as a quick 'cheat sheet' to help you remember the required commands.

## Basics
  * `$ git init`: creates a new git repo, with data stored in the (hidden) '.git' directory
  * `$ git status`: tells you what’s going on - current status of the repo
  * `$ git add <filename>`: adds specific file to the staging area
    * `$ git add .`: adds all files to staging area
  * `$ git commit`: creates a new commit
  * `$ git commit -m "Commit message"`: creates a new commit with 'message'
  * `$ git commit -a`: creates a new commit for all available files (careful!)
    * will only commit files that are already being tracked. Use `$ git add .` first to also add any new files
    * Will open whichever text editor git has set up as default for you to enter a commit message. You can change the default editor, e.g.:
      * `$ git config --global core.editor "gedit"`
      * `$ git config --global core.editor "vim"`
  * `$ git commit -a -m "Commit message"`: adds all changed files and creates a new commit, with 'message'
  * `$ git log`: shows a flattened log of history
     * `$ git log --graph --pretty --oneline`: Nice way to visualise history as a graph (without 'oneline' to get full details)
  * `$ git diff <filename>`: show changes you made relative to the staging area
  * `$ git diff <revision> <filename>`: shows differences in a file between snapshots
  * `$ git checkout <revision>`: updates HEAD and current branch
     * revision can be a name (branch name), or the hash of a specific commit

### FAQ:
  * Why do I need to "stage" and then "add" - why isn't this one step
    * While it is common to want to commit _all_ the changes you have made in one go, it's also common for us _not_ to want to do this. Having a two-step process allows us to commit some of the changes we have made, without committing others. (You can even selectively commit only part of a file)
    * If you want to do both in one step, you may use `$ git commit -a -m "Commit message"`

## Branching and merging
  * `$ git branch`: shows branches
  * `$ git branch <name>`: creates a branch
  * `$ git checkout -b <name>`: creates a branch and switches to it
     * (same as `$ git branch <name>` followed by `$ git checkout <name>`)
  * `$ git merge <revision>`: merges '<revision>' into current branch

## Remotes (push, pull)
  * `$ git clone <remote-url>`: download repository from remote
  * `$ git remote`: list remotes
  * `$ git remote add <name> <url>`: add a remote (default remote name is 'origin')
  * `$ git push <remote> <branchName>`: send objects to remote, and update remote reference (default remote name is 'origin')
    * e.g.: `$ git push origin main` pushes to remote version of 'main'
  * `$ git fetch`: retrieve objects/references from a remote
  * `$ git pull`: Pulls changes from remote branch into yours

## Undo commits (keep changes to files)
  * `$ git commit --amend`: edit a commit’s contents/message (careful!)
    * This should essentially never be done if a commit has already been pushed to the remote
  * `$ git reset HEAD <file>`: unstage a file
  * `$ git reset HEAD~1` : undoes last 1 commit (keeps file changes)

## Undo commits and changes **CAREFUL**
  * `$ git checkout -- <file>`: discard all changes to file <file>
    * **careful**: cannot be undone
  * `$ git reset --hard` : discards all changes since last commit
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

### Example .gitignore file:

Here, I'll give three common examples.


 **1.** Ignore specific files:

For example:
```
*.log
*.aux
*.out
*.synctex.gz
```
* Ignores all .log, .aux, ..etc. files


**2.(a)** Ignore everything, except (basic):

```
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


```
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
