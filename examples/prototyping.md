# Efficient Prototyping

This application is actually often use as the "selling point" of git. Other just
consider it one of the most common workflow (assuming we leave out the "I don't
really understand what I am doing so I am just commiting linearly" workflow"):
branching and merging!

The idea in a nutshell is:

* Your master branch is always clean.

* When you want to work on a new feature or add something to your code, you
  create a "branch" and work on your feature in isolation.

* Once the feature is complete, you "merge" the branch you created with the
  master branch.

* git takes care of merging the commit history of your side branch with the
  master branch so it now looks like the whole work was made in the master
  branch all along (unless you inspect `git reflog` of course).

## Branching

Assume we have a repository which looks like this:

	A -> B -> C -> D  <= master <= HEAD

where `A`, `B`, `C` and `D` are the only 4 commits in your repository. You only
have the default branch, "master", and the current state of your repository (the
position of "HEAD") is pointing to "master" and so what you see in the
repository is the content of the repository after commit `D`.

We might want to work on a new feature without making the master branch
unusuable during development. Thus, let us create a new branch:

	git branch prototype

We can inspect all available branches using:

	git branch

which should display:

	* master
	  prototype

telling us we are still on branch "master" but that there exists another branch
prototype. Visually it looks like this:

	A -> B -> C -> D  <= prototype  <= master <= HEAD

To start working on the new branch, we need to switch our HEAD to it:

	git checkout prototype

yielding:

	A -> B -> C -> D  <= prototype <= HEAD  <= master

Nothing very exciting until we actually commit something to it. Assume we go
ahead and make 3 more commits (`E`, `F` and `G`):

	A -> B -> C -> D  <= master
	               |
		       -> E -> F -> G  <= prototype <= HEAD

That looks good; the prototype is coming along nicely. But a user just reported
a bug on the master branch that requires immediate attention:

	git checkout master
	[...]
	git commit -a

and now we have:

	A -> B -> C -> D -> H  <= master <= HEAD
	               |
		       -> E -> F -> G  <= prototype

We were able to fix the urgent bug without leaving the repository in a weird
state and without compromising the work we did on the prototype branch. Now all
there is left to worry about is how to combine the work on the master branch
(which now include a bugfix in commit `H`) and the prototype branch...

## Merging

Merging is the action by which git will replay the commit history of a specified
branch in the current branch.

Let's assume the prototype we developed in the previous section is now ready to
deploy after commit `G`:

	git merge prototype

Our commit history will now look like this:

	A -> B -> C -> D -> H --------> I  <= master <= HEAD
	               |            |
		       -> E -> F -> G  <= prototype

What happened? A new commit `I` was created which is the result of applying
commit `E`, `F` and `G` from commit `H`.

Git use an elaborate merging algorithm so that user intervention is only needed
if 2 (or more) commits in different branches modify the exact same code. In
which case the operation will be aborted, git will print an error message
indicating which files' sections are in conflict and annotating those same files
for the users to "merge" manually. Once the user is satisfied with his manual
merging, he/she can run `git commit` again to finalize the merging operation.

Note that the prototype branch still exists and still point at commit `G`. If
you are not going to ever develop from commit `G` again, simply remove it using
`git branch -d prototype`.

