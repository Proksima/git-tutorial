# Git Tutorial

The goal of this tutorial is to introduce you to git with practical applications
so that it becomes an integral part of your workflow.

Git is a distributed version-control system. You should typically use such
system to manage any data for which:

* You want to track (and potentially revert) changes.

* You want to maintain multiple versions of.

* You want to distribute with the possibility of merging back the distributed
  changes at a later time.

While this introduction may feel abstract, it will get more concrete as we go
through the basics and concrete applications I decided to include in this
tutorial.

## Basics

### New Repositories & Cloning

Creating a new repository is as simple as running

	git init

to initialize it in the current working directory. Alternatively, you can
provide a path to the directory where you want to initialize the repository.

You will notice it creates an hidden directory named .git. This directory
contains all the metadata git needs to maintain the repository.

Alternatively, if you want to clone an existing repository, you can do so by
running

	git clone https://github.com/Proksima/git-tutorial

where the URL given as example is the repository holding the material for this
very tutorial. Note that it needs not to be an URL, it could be a local
repository specified by a path. A repository could also be cloned over the SSH
protocol. As an example, the following command would be equivalent to the last
one

	git clone ssh://dlevac@mimi.cs.mcgill.ca:~/repositories/git-tutorial

assuming you know my CS password...

### Tracking Files & Commiting Changes

By default, no files is tracked by git in a newly initialized repository, the
repository is just empty. Let's create a dummy project to show how we would add
files to the repository.

	mkdir ~/git-example
	cd ~/git-example

	git init
	touch main.c

	git add main.c

Now we have a repository with only 1 tracked file. If you type

	git status

you should see the following:

	On branch master

	Initial commit

	Changes to be committed:
  	  (use "git rm --cached <file>..." to unstage)

	        new file:   main.c

basically telling us that we have a new file in the repository waiting to be
commited. At any point, if you change your mind and decide you want to flush the
changes you made since the last commit, running `git checkout master` will do
the trick. We will see next section why that is.

For now, I am happy with this change, so I will be committing it:

	git commit

This will open my favorite text editor so I can insert a commit message,
describing the changes I've made. Once the commit is done, the state of the
repository at the time of the commit will be immortalized and I can continue
my work.

Now I could decide to create a new file and make changes to my main.c files:

	touch todo.txt
	vim main.c

After which `git status` would display:

	On branch master
	Changes not staged for commit:
  	  (use "git add <file>..." to update what will be committed)
  	  (use "git checkout -- <file>..." to discard changes in working directory)

		modified:   main.c

	Untracked files:
  	  (use "git add <file>..." to include in what will be committed)

		todo.txt

Whoops, we forgot to use `git add` to both

* Tell git we want to commit the changes made to main.c.

* Add todo.txt to the files git should be tracking.

Fortunately git tells us what to do and running `git add main.c todo.txt` will
do the trick, after which we can run `git commit` to actually commit the
changes.

Alternatively, running

	git commit -a

will automatically commit the changes in every tracked files in the repository.

### Branching & Merging

### Commit History

### Backtracking

## Distributed Environments

## Managing Datasets

