Git Tutorial

To use this repo you should do the following:

* Fork the repo on github.
This gives you your own copy to mess about with.
The copy here is the 'official' source and can't be changed directly.
At this point you'll have a copy of the repo on github, but that's not much use for coding...
Press the 'fork' button in the top right-hand side of github.

* Clone your repo.
This will download a copy of your personal repo onto your computer.
You can use this to start hacking.
On your computer run the command:
  git clone git@github.com:<your-username>/git-tutorial.git

ie if your username is 'iloverobots' then you would run:
  git clone git@github.com:iloverobots/git-tutorial.git

You'll end up with a directory called git-tutorial.
This is where you do your work.

* Set up a link to the master repo.
By default your personal repo on github is the 'origin'
We also want to be able to get other people's changes from the master repo.
We do this by adding a 'remote' in git parlance. We already have a default
remote (called 'origin').
Run this command:
  git remote add dropbears git@github.com:thedropbears/git-tutorial.git

This will add a remote called 'dropbears'.

* Do some work.
You should always work on a branch, and not on master.
Master is where we go when we have finished.

But first we check that master is up to date with the official repo (ldu):
  git pull dropbears master
That tells git to get all the changes from the remote 'dropbears' and the branch 'master' on that remote.

Now we create a new branch to do our work:
  git checkout -b new-feature
This creates a branch called 'new-feature'. You can have as many branches as you want.

We do our stuff.
Edit the file called 'names.txt' and add your name.
Also create a subdirectory with your name and put something in it.

We need to save our work. We call this 'committing'. Each commit is a change that we've made.
Don't bunch different changes together - each commit should refer to only one self-contained change.
Bunching heaps of stuff together is called patch-bombing and it's bad.
We want commits to be small so we can review and understand them and reject ones we don't like
without getting rid of all the other changes.
You can't accept part of a commit - it's all or nothing.

Let's commit:
  git add names.txt
  git add my_directory/*
  git commit -m "Added my name to the names file. Created a directory."

The first two lines tell git which changed files we want included in our commit.
The third line makes the commit. The -m flag adds a message.

Have a look at the log:
  git log

Your commit should be there.

* Rebase and merge.
It is possible that while we have been working someone has made a change to the dropbears repo.
We want our commits added to the end of that, otherwise stuff gets confusing.

Check for updates to ldu:
  git fetch dropbears

Put our changes at the end of the master branch on ldu (that we just updated).
  git rebase dropbears/master

You should do this periodically when you are working to make any conflicts easier to resolve.

* Push to your repo
Up to now, all of your changes are on your computer. You need to put them where people can see them
and integrate them into their work.
You 'push' them up onto your personal repo on github.

  git push

By default git push pushes to origin (your repo).
You can also do:
  git push <remote> <branch>
to push to a specific remote.

* Get your work onto the main repo.
Send a pull request to your Section Leaders.
You can do this via github, or email or on IRC. We normally use email, and not GitHub.

* That's it!
The short version of this is:
Pull from the main repo (dropbears), and push to your personal repo.
Then one of the admins will pull your changes from your repo onto the main (dropbears) repo.
Keep your repo up to date as you work with plenty of 'git fetch dropbears' and rebase your work with
'git rebase dropbears/master'
Push your work (still on your branch, not on master!).

* Cleaning up
After your commits have been accepted and put onto the master branch of 'dropbears' you
can delete your local topic branch and the topic branch on your GitHub fork.
Change back to the master branch:
  git checkout master
Pull from 'dropbears':
  git pull dropbears
Delete your local branch:
  git branch -D new-feature
Delete branch on your fork:
  git push origin :new-feature


* Further reading
http://git-scm.com/book

* Suggestions
Feel free to edit this, and make a pull request if you think it could be better! ;)

JRW
02 Nov 13
