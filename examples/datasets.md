# Managing Datasets

When we think about revision control, we often think about code. However, it can
really be used for any kind of data. Here I want to tackle the problem of
managing datasets. Git can help you in multiple ways:

* By providing version-control (betcha you didn't see that one coming!)

* By allowing you to modify the dataset in different ways in different branches.

* By allowing you to easily clone a specific branch (maybe to run an experiment
  on a more powerful machine?)

Before getting started, we have some preliminary work to do.

## Git LFS

Unfortunately, out of the box, git is not very good with very large files;
especially binaries. If you are working with big data, you will want to install
the [Git Large File Storage](https://git-lfs.github.com) extension.

Follow the steps for "Getting Started" in your dataset repository (you might
need to "invent" a custom extension for the filenames so that `git lfs` can
track them).

## A CS-Specific Use-Case

A lot of researchers at McGill hold their datasets in their home directory. Home
directory at CS are on an NFS share. This means I/O operations are actually
network operations when performed in the home directory. In other words, running
an I/O intensive task on a dataset in your home directory will make your
experiment network-bound on top of clogging network resources from your
colleagues.

Let us use git to help to manage and run an I/O intensive experiment on a
dataset that usually reside on a network share:

	mkdir ~/example-dataset
	cd ~/example-dataset

	git init
	git lfs install
	git lfs track "*.data"  # could be any extension, e.g. ".json"

	git add .gitattributes
	git commit -m "Initial commit with LFS support."

Now let us create a dummy dataset to add to the repository (or use a real one if
you have one on hand!)

	for IDX in $(seq 1 10)
	do
		head -c 10000 /dev/urandom >> $IDX.data
	done

	git add *.data
	git commit -m "Added 10 dataset files to the repository."

Let us say we want to run an I/O intensive task on the dataset on
`agent-server-1.cs.mcgill.ca`. There is local storage available to everyone in
the /NOBACKUP directory on that server.

	ssh dlevac@agent-server-1.cs.mcgill.ca
	git clone ssh://dlevac@agent-server-1.cs.mcgill.ca:~/example-dataset /NOBACKUP/example-dataset

	cd /NOBACKUP/example-dataset

Now we have a copy of the repository we can use on the local disk of
agent-server-1. In the event we had multiple branches, we could have cloned that
only branch (and nothing else) by appending the `git clone` command with the `-b
BRANCH_NAME --single-branch` options.

Once our experiment is done:

	git commit -a
	git push

which will create a new commit with the modifications to the dataset and then
"push" it back to the original repository we cloned from.

Alternatively, you can `git pull` from the original repository by specifying the
full path over the SSH protocol to the repository on agent-server-1's local
disk.

