# Cheatsheet

## Initialization

* `git init` to create a new repository under the current directory.

* `git clone` to get a local copy of a repository.

## Local Operations

* `git add` to tell git the specified file(s) should be included in the next
  commit.

* `git commit` to commit the "staged" changes in the repository. Use the `-a`
  option to automatically stage all tracked files that were modified.

* `git revert` will commit the inverse of the specified commit, effectively
  "cancelling it out".

## Displaying Information

* `git status` get information about the current state of the repository.

* `git log` get the (public) commit history of the repository.

* `git reflog` get the (local) history of operations on the repository.

## Branching

* `git branch` will either enumerate all available branches without argument, or
  create a new branch with the name specified as argument.

* `git checkout` will switch to the specfied branch (the default branch is
  called "master").

* `git merge` will merge the specified branch in the current branch.

## Remote Operations

* `git remote add origin` specify the default remote copy of the repository to
  use when "pushing" or "pulling" (not needed if the repository was created
  using `git clone`).

* `git pull` query the latest changes from the default remote repository
  ("origin") and apply them to the current branch. (You can optionally specify
  which remote to query into which branch, e.g. `git pull origin master`.)

* `git push` push your local change to the default remote repository. (I didn't
  actually cover `git push` but it is common enough to show here.)

## LFS Support

* `git lfs install` will setup the LFS extension in the current repository.

* `git lfs track` will track the files that satisfies the provided regular
  expression (make sure your ".gitattributes" file is tracked by git after this
  step).

