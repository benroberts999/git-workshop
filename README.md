Some helpful tips for students in our group:

## Getting started
  * Install:
     * $sudo apt install git    (ubuntu)
     * $brew install git        (mac)
  * plugins available for most code-focussed text editors (e.g, Atom)
  * git help <command>: get help for a git command
  * There are GUI versions - but command-line is more useful

## Basics
  * git init: creates a new git repo, with data stored in the .git directory
  * git status: tells you what’s going on
  * git add <filename>: adds files to staging area
  * git commit: creates a new commit
  * git commit -m "Commit message": creates a new commit with 'message'
  * git commit -a: creates a new commit for all available files (careful!)
  * git log: shows a flattened log of history
     * git log --all --graph --pretty: Nice way to visualise history as a graph
  * git diff <filename>: show changes you made relative to the staging area
  * git diff <revision> <filename>: shows differences in a file between snapshots
  * git checkout <revision>: updates HEAD and current branch
  New line

## Branching and merging
  * git branch: shows branches
  * git branch <name>: creates a branch
  * git checkout -b <name>: creates a branch and switches to it
     * (same as git branch <name>; git checkout <name>)
  * git merge <revision>: merges into current branch

## Remotes (push, pull)
  * git clone: download repository from remote
  * git remote: list remotes
  * git remote add <name> <url>: add a remote
  * git push <remote> <local branch>:<remote branch>: send objects to remote, and update remote reference
    * e.g.: git push origin master
  * git fetch: retrieve objects/references from a remote
  * git pull: Pulls changes from remote branch into yours (same as git fetch; git merge)

## Undo commits (keep changes to files)
  * git commit --amend: edit a commit’s contents/message (careful!)
  * git reset HEAD <file>: unstage a file
  * git reset HEAD~1 : undoes last commit (keeps file changes)

## Undo commits and changes **CAREFUL**
  * git checkout -- <file>: discard changes
  * git reset --hard : discards all changes since last commit


## gitignore
  * Not needed, but handy
  * List file patterns in ".gitignore" (with the '.' in filename) that you don't want git to track
  * Handy: want to track some but not all files (don't want to track compiled code, log files etc.)
  * lines beginning with '!' means 'except'.
    * I like to tell it to ignore everything (use "*"),
    * except for certain files (example: "!*.cpp")


### Example .gitignore file:

 1) Ignore everything except:

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

 2) Ignore specific files:

```
*.log
*.aux
*.o
```

 * Ignores all .log, .aux, .o files
