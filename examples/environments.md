# Distributed Environments

Here I want to discuss another place where version-control shines in utility but
is rarely used in practice: distributed environments.

If you are the kind of person which takes hours to setup your programming
environment to be of your liking, why not do it once and then put it into
revision control? This allows you to keep a stable and reproductible environment
across multiple workstations, and if anything happen, you can revert undesired
changes to your environment.

To illustrate this concept, I chose an environment that everybody uses: home
directories.

## Placing your Home Directory under Git

Here at McGill, your home directory is on an NFS share and so, all your files
are available on every CS machine. However, you might want your setup to follow
you on your home machine.

Let us initialize a new repository in our home directory and track some files:

	cd
	git init

	git add .bash_profile         # script ran when a shell is spawned
	git add .bashrc               # same as .bash_profile
	git add .bash_logout          # script ran when a shell is exited
	git add .gitconfig            # your git configuration file
	git add .screenrc             # customization for GNU/screen
	git add .ssh/id_rsa           # your private SSH-key
	git add .ssh/id_rsa.pub       # your public SSH-key
	git add .ssh/authorized_keys  # (public) SSH-keys allowed to login
	git add .vimrc                # your VIM configuration file

	git commit

It is a safe and convenient way to share those files, some sensitives, and to
maintain them across multiple workstations. You also have the hidden advantage
of being immediately warned by git if one of the file change (all files under
git have a checksum).

Now, lets say I am starting work at a new company, and I am provided with a
fresh Linux install and I'm told to set it up how I like. I can simply

	cd
	git init
	git remote add origin ssh://dlevac@mimi.cs.mcgill.ca:/~
	git pull origin master

and all my home directory customization will follow me.

Now you might wonder why I didn't just `git clone`. This is a particularity of
this example: `git clone` forces the creation of a new directory, but the home
directory already exists. Thus, I need to initialize an empty repository and
tell it where the "source" is for populating itself.

## A Note About Anaconda

Some of you might be using Anaconda to get a self-contained Python environment.
Unfortunately, Anaconda does not support being moved around (the path to the
root of the Anaconda setup must not change). Together with the fact it uses a
lot of binaries, it might not be the best candidate to be put into revision
control.

If you do wish to still put your environment under git, look into the "Managing
Datasets" section to learn about managing binaries and big files with `git lfs`.

