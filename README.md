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

### Branching & Merging

### Commit History

### Backtracking

## Distributed Environments

## Managing Datasets

