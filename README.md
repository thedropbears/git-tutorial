# Git Tutorial

To use this repo you should do the following:

## Clone the repo

This will download a copy of the repo onto your computer.
You can use this to start hacking.
On your computer run the command:

```bash
  git clone git@github.com:thedropbears/git-tutorial.git
```

You'll end up with a directory called git-tutorial.
This is where you do your work.

## Do some work
You should always work on a branch, and not on main.
main is where we go when we have finished.

But first we check that our local copy main is up to date with the remote repo (origin):

```bash
  git pull origin main
```

That tells git to get all the changes from the remote `origin` and the branch `main` on that remote.
In this case `git pull` would also suffice as by default it has the parameters `origin` and `main`, however, once you have branched this will be replaced with `origin` and `branch_name`

Now we create a new branch to do our work:

```bash
  git checkout -b new-feature
```

This creates a branch called `new-feature`. You can have as many branches as you want.

We do our stuff.
Edit the file called `names.txt` and add your name.

We need to save our work. We call this 'committing'. Each commit is a change that we've made.
Don't bunch different changes together - each commit should refer to only one self-contained change.
Bunching heaps of stuff together is called patch-bombing and it's bad.
We want commits to be small so we can review and understand them and reject ones we don't like
without getting rid of all the other changes.
You can't accept part of a commit - it's all or nothing.

## Let's Commit

```bash
  git add names.txt
  git commit -m "Added my name to the names file"
```

The first two lines tell git which changed files we want included in our commit.
The third line makes the commit. The -m flag adds a message.

Have a look at the log:

```bash
  git log
```

Your commit should be there.

## Rebase and merge.
It is possible that while we have been working someone has made a change to the dropbears repo.
We want our commits added to the end of that, otherwise stuff gets confusing.

Check for updates to the main:

```bash
  git fetch origin
```

Put our changes at the end of the main branch (that we just updated).

```bash
  git rebase origin/main
```

You should do this periodically when you are working to make any conflicts easier to resolve.

## Push to the repo
Up to now, all of your changes are on your computer. You need to put them where people can see them
and integrate them into their work.
You 'push' them up onto your the repo on github.

```bash
  git push
```

By default git push pushes to origin your_branch.
You can also do:

```bash
  git push <remote> <branch>
``` 

to push to a specific remote.

## Get your work onto the main repo.
Send a pull request to your Section Leaders.
You can do this via github, or email or on IRC. We normally use email, and not GitHub.

## That's it!
The short version of this is:
Pull from the main repo (dropbears), and push to your personal repo.
Then one of the admins will pull your changes from your repo onto the main (dropbears) repo.
Keep your repo up to date as you work with plenty of `git fetch dropbears` and rebase your work with
`git rebase dropbears/main`
Push your work (still on your branch, not on main!).

## Cleaning up
After your commits have been accepted and put onto the main branch of 'dropbears' you
can delete your local topic branch and the topic branch on your GitHub fork.
Change back to the main branch:

```bash
git checkout main
```

Pull from 'dropbears':

```bash  
git pull dropbears
```

Delete your local branch:

```bash  
git branch -D new-feature
```

Delete branch on your fork:

```bash
git push origin :new-feature
```

## Further reading
http://git-scm.com/book

## Suggestions
Feel free to edit this, and make a pull request if you think it could be better! ;)

JRW
02 Nov 13
