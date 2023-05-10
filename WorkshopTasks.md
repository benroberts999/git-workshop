# Workshop Tasks
adding a change but on a branch!
## Pre-work

* Make yourself a github user account <https://github.com>
* Install Visual Studio Code: <https://code.visualstudio.com/>
* (optional) If you want to use the command line, set up ssh keys: <https://docs.github.com/en/authentication/connecting-to-github-with-ssh>

## Tasks

1. **Fork** the repository <https://github.com/benroberts999/git-workshop> on github

* click the 'fork' button

2. **Clone** your version of the repo to your pc

* Command line: `git clone <repo-name>`
* Or, chose "clone repository" from the "source Control" tab in VSCode (cntl+shift+g)
* As an alternative to 1 and 2, simply clone a copy of my repo. If you want to publish the changes to your github account, you'll have to create an empty repo on github.com, and update the 'remote' address of this repo to point to that one
  * `git remote add origin <your_repo>`

3. **Make some changes** in the repository (don't commit them yet)

* For example, add a new line to the README file, or add a new text file
* Use `git diff` (or the source controll tab) to see your changes

4. **Stage and commit** your changes

* `git add <...>`
* `git commit -m <your commit message>`
* Or, commit using the source controll tab in VSCode

5. **Push** changes up to your github 'remote', and look at changes on github.com

* `git push origin main`

6. Make some other **change on github.com**

* You can edit a file by clicking the `edit` button (pencil); commit directly to main

7. **Check for those changes on your pc**

* First, run `git status`; it should say "up to date", because is doesn't know about the upstream changes
* Run `git fetch`, and then do `git status` again; now it says there are changes
* Run `git pull` to get those changes on your pc
* This can all also be done from the source controll tab in VSCode

8. **Branch.** Make a new branch, and commit some changes on it. Swap back to original branch

* `git branch <branchname>`
* then: `git checkout <branchname>`
* Or: `git checkout -b <branchname>` (does both at same time)
* Then make changes and commit them as before
* `git log` (or `git log --graph --oneline`)
* push this branch up to github.com: `git push origin <branchname>`, or `git push --set-upstream origin <branchname>`
* Swap back to original branch: `git checkout main`

9. **Merge** branch

* `git merge <branchname>` merges the changes and commits from new branch "branchname" into current branch.
* It is simplest if there are no changes on the incoming branch.
* If there are changes on both branches, but to different parts of the code, git is smart enough to merge the changes with a new commit on its own
* Sometimes, the merge cannot happen automatically if there are changes on both branches to the same parts of the code: in that case, you have to manually

10. (optional) **Merge Confict**

* If you're feeling very adventurous, try to create a merge confict
* Do this by repeating steps 8 and 9, but this time make and commit changes to _both_ branches before the merge
* I highly recommend using VSCode (or similar) graphical interface for merge conflicts, unless you really enjoy painand suffering
