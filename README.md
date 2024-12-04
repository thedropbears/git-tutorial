# Git Tutorial

This guide serves as a brief outline on the Team's git workflow. If you follow along you will likely have exercised using all the commands we commonly use. You also get to add your name to our 'guest book' so people know you were on the team at some point!

The broad steps for working in the team are:

- Clone the code (Download)
- Do some Work
- Commit your code (Save)
- Clean your History (Rebase)
- Push your code (Upload)
- Make a pull request (Review and Merge)
- Clean up

## Clone the Repo

Cloning is a special form of download within git. It is a process for registering your download for later reuploading and contributing to a code project.

Run the following command in a terminal instance to clone this repo:

```bash
git clone git@github.com:thedropbears/git-tutorial.git
```

You can break this down into a series of keywords to better understand the operation

- git -> The primary command word to execute the git program
- clone -> the subcommand so we are about to clone something
- the url -> the online repository to download the code from, in this case it is this tutorial repository

You'll end up with a directory called git-tutorial where you called the clone operation. This is where you do your work.

**NOTE: Make sure you run this clone command in a known location and one that you want to work in going forward.**

**When opening a terminal from the applications menu, it will open in your home directory by default. The absolute path of this on Windows is normally `C:/users/<your user name>` and `/home/<your user name>` on Linux/MacOS. It will contain folders for your `Desktop`, `Documents`, `Downloads`, etc. We suggest moving to a place you can more easily access because you will be using it a lot!**

**Use and adjust the following to suit your preferences:**

``` bash
ls # ls stands for list to check what files and folders are at the current location.
# Check you really are in home!
cd Desktop # cd stands for change directory. We are changing directory to the Desktop
mkdir robotics # mkdir stands for make directory. We are making a new directory called robotics on the Desktop
cd robotics # change into the newly created robotics directory
```

Now you can run the `clone` command to create a copy of the repo in the directory you just navigated to.

## Do Some Work

When using git, we work on 'branches'. Branches are a series of different save states of code with potentially different change history. The default branch, often called `main`, is the most up to date source of truth, with current reviewed and working code. We never work directly on the main branch, instead we create other branches dedicated to issues or new features. Any new branch can then be merged into the `main` branch to update it with the new source of truth.

Start by ensuring we are on the default branch. This will be the point we make a new branch from.

```bash
git checkout main
```

Breaking this down:

- git -> Keyword to execute git program
- checkout -> Command to change to a new branch
- main -> Branch to switch to

We must check that our local copy of main is up to date with the upstream repository.

```bash
git pull origin main
```

Once again we can break this down:

- git -> Keyword to execute the git program
- pull -> Command to download new changes from the remote repo and apply them if it can
- origin -> Parameter specifying the remote (online) repository. Origin is special and will be wherever you cloned the repo from
- main -> Second parameter specifying the branch to get from a remote. In this case we are pulling from main

Running `git pull` alone would also work in this case for a first time clone. Without the extra parameters, the command assumes the origin remote and whatever branch you are currently on. A freshly cloned repository will be on the default branch, which is `main` for us.

Now we can create a new branch to do our work:

```bash
  git checkout -b new-feature
```

- git -> Keyword to execute git program
- checkout -> Command to change to a new branch
- -b -> Extra parameter specifying to create a new branch while changing
- new-feature -> Branch to switch to

When naming branches, there are a few guidelines that should be followed:

- Names should reflect what work will be happening in the branch
- Names should not contain spaces or other strange characters, replace any spaces that may be needed with - or _
- Make the name short and to the point
- Names should be prefixed with your name

For this branch you should call it `<your_name>/add_name_to_repo`

Now we can make our changes. Edit the file called `names.txt` and add your name.

## Commit Your Code

<!-- Mention that is isnt enough just to save the changes to share them -->
<!-- Enter the commit! -->
<!-- Commits can and should often contain changes to multiple files if they are a part of the same change -->
<!-- Commits should still remain small and self contained to a single change -->
<!-- People will often view and track the commit history to contextualise the evolution of a project -->

<!-- Start by doing a git status to see what files have been changed -->
<!-- note that things are unstaged so they wont be added to a commit when we try to do it -->
<!-- We are only expecting to change the names.txt file, make sure to undo anything else! -->
<!-- stage the change with git add -->
<!-- run git status again and note the change is now staged-->
<!-- commit -->
<!-- breakdown commit command -->
<!-- make sure to add that there is a coupling between -m and the following string -->

<!-- note that it is important to have a meaningful commit message -->
<!-- add some sassy shade on how people do read these things and how it can reflect the quality of the programmer when its just junk -->

<!-- inspect the command with git log -->
<!-- add note on usage of gitk/gitg to visualise the git graph. gitk is installed by default on windows with a git bash install. Mac and linux users will need to install one themselves -->
When working with git, it isn't enough to just save your files to share them with the rest of the repository. In order to share changes, commits must be made. A commit is essentially a save checkpoint, which denotes the changes that have been made to the file.

Commits should be contained to single changes and made often. People will often look at the commit history to contextualise and grasp an understanding of the changes that have been made within your working branch. **Note: This does not mean that commits cannot contain multiple files, in fact they should if they are part of the same change.** 

Once we have made our changes, we must first check what files have been modified. To do this, run:

```bash
git status
```

When committing files, modified files will be `staged` or `not staged` for a commit. Staged files will be contained within the next commit, whilst not staged files will be ignored.

Once `git status` is run, it will show the files that have been modified but are currently unstaged and those that are staged. As we have only modified the names.txt file, it will appear as unstaged and should be the only modified file.

To stage the file for commit, we run:

```bash
git add names.txt
```

This will `stage` the `names.txt` file for committing in the next stage. Running `git status` again should now show the `names.txt` file as staged and ready to commit.

Now we can make a commit by running:

```bash
git commit -m "added my name to the names file"
```

- git -> Keyword to execute git program
- commit -> Command to create a snapshot of the currently staged changes within the branch timeline
- -m -> Extra parameter specifying that the commit will contain a message string following it
- "added my name to the names file" -> The commit message string 

When you make your first commit in a repository, it will ask you to set your name and email. These will be signed on your commits, showing it was you that made them. To set your name, run `git config user.name "<Your Name>"` and to set your email run `git config user.email "<Your Email>"`

When making commits, it is extremley important to have clear and meaningful commit messages, people read commits to understand what is happening in the code. The difference between a good and ok programmer can be seen in the quality of their commit messages. 

Now that we have made our commit, we can check the commit history using `git log`, this will show all commits within the history of the branch, including those from `main` before you created the branch. If you go all the way back, you can see the first commit made to this repository by James Ward in 2013.

If you prefer a more visual interface for viewing commit histories, as well as viewing the changes made in each commit, you can use a program called gitk. For windows users, gitk comes bundled with git.

For Mac users, run `brew install git-gui` to install gitk

For Linux users, run `sudo apt-get install git-gui gitk`

To use gitk, in a terminal run `gitk` to view the view the current branches history or `gitk --all` to view all repository commit history.

## Clean Your History

<!-- We believe that code should always be done with respect to the latest main -->
<!-- History may have progressed in the time its taken you to write your feature or solve an issue -->
<!-- Rebasing is a way of replaying a series of commits off another set of history as if it was done that way the whole time -->
<!-- Sounds nice in theory but you will get conflicts if you and someone else have touched the same parts of code -->
<!-- Some of you will have to deal with this right now! -->

<!-- start by fetching -->
<!-- break down the command -->
<!-- identify it is different to pull because it will not do a merge -->
<!-- the remote branch and the local branch may now not be aligned. This is ok -->
<!-- use gitk/gitg to visualise this to see if its true -->

<!-- rebase off origin/main just in case-->

<!-- resolve the merge conflict if if there is one -->
<!-- git status will now show which files have merge conflicts -->
<!-- git will display two versions of history, current and incoming -->
<!-- current is what is in main now and incoming is your set of changes -->
<!-- you can accept one, the other, both or do something totally different to solve the problem -->
<!-- remove the extra junk characters and fix the change to how it should be -->
<!-- Remember the intent here is to add your name to the log and not delete anyone elses entry -->
<!-- Stage the resolved conflict  -->
<!-- continue the rebase -->

<!-- You should try to regularly rebase while developing to avoid a build up of conflicts. -->
<!-- It can be really hard to solve if too much has changed while waiting for your feature -->

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

<!-- changes are only on your local machine right now -->
<!-- they need to be uploaded before anyone else can review and add your code to the default branch -->
<!-- enter le git push -->
<!-- break down the command -->
<!-- git will reject the push the first time because it doesnt know where to push to -->
<!-- Follow the terminals instructions and add the --set-upstream things -->
<!-- break down the command -->

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

## Get your work onto the main repo

<!-- Make le PR -->
<!-- use the link generated in the terminal if its the first time pushing -->
<!-- Otherwise go to github ->pull requests ->new pr -> set proper base and target branch -->
<!-- Let someone know you have made a pr, tag tyhem as a reviewer, message them on slack or send an email -->
<!-- people should be checking email and slack regularly as the common modes of comm on the team but slack might be faster in most cases -->

Send a pull request to your Section Leaders.
You can do this via github, or email or on IRC. We normally use email, and not GitHub.

## That's it

<!-- I think we can remove this in its current form -->

The short version of this is:
Pull from the main repo (dropbears), and push to your personal repo.
Then one of the admins will pull your changes from your repo onto the main (dropbears) repo.
Keep your repo up to date as you work with plenty of `git fetch dropbears` and rebase your work with
`git rebase dropbears/main`
Push your work (still on your branch, not on main!).

## Cleaning up

<!-- once the branch is merged you can prepare your main for the next feature -->
<!-- checkout -->
<!-- pull -->
<!-- and delete the local branch -->
<!-- Break down the command -->
<!-- Note the capital D. It is important vs a lowercase one. I challenge you to read the docs @Asher and find out why. I am going to quiz you on it :p -->
<!-- We have auto delete setup for upstream things so they dont need to worry about that anymore -->

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

[The definitive book guide for git!](http://git-scm.com/book)

## Suggestions

Feel free to edit this, and make a pull request if you think it could be better! ;)

LM 03 Dec 24
JRW 02 Nov 13
