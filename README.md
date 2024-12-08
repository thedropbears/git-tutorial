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

It isn't enough to just save your files to share them with the rest of the team. We must go through the process of commiting instead. A commit can be thought of as a save checkpoint designated when changing one or many files. A commit is also accompanied by a message outlining what was changed in the process.

It is common to make many commits on a single branch when writing a new feature or fixing an issue. Commits should be small and made often. People will often look at the commit history to contextualise all of the changes made on a branch to accomplish a feature or fix. Commits can and should contain changes to multiple files at once if they are a part of the same change. This doesnt mean you should implement one massive feature altering the entire codebase in a single commit. That is called patch bombing, and it is bad. It makes things very hard to review which only slows down the cadence of development.

Now that we have made our changes, it is often a good idea to first double check that there are only changes where we expect them. We do this with:

```bash
git status
```

`git status` will show files in three states; untracked when git sees something new that it doesnt know about yet, unstaged when there are changes to files that git knows about that wont be included in the next commit and staged for files that git knows have changed and will be included in the next commit. Anything else is considered unchanged or ignored.

We are only expecting changes to the `names.txt` file. It should come up as unstaged because it is already in git's version control. To stage it run the following:

```bash
git add names.txt
```

It is possible to stage multiple files at once with wildcards (the `*` operator), so `*.txt` would stage all txt files at once if there were others but in this case it is better to be explicit.

`names.txt` should now be staged. Check this by running `git status` again. if it is you are now ready to commit with:

```bash
git commit -m "added my name to the names file"
```

- git -> Keyword to execute git program
- commit -> Command to create a snapshot of the currently staged changes within the branch timeline
- -m -> Extra parameter specifying that the following string will be the the commit message
- "added my name to the names file" -> The commit message 

When you make your first commit in a repository, it will ask you to set your name and email. This information forms part of the commit meta data so everyone can see who made the change. Follow the instructions in your terminal and run

``` bash
git config user.name "<Your Name>"
git config user.email "<Your Email>"
```

Commits must have clear and meaningful commit messages! People read commit messages to understand what is happening in the code for review and very likely again 6 months later when trying to understand why a change was even necessessary. The quality of programmer is very clearly refected in the quality of their commit messages, so try to make them good! 

Now that we have made our commit, we can check the commit history using `git log`, this will show all commits within the history of the branch, including those from `main` before you created the branch. If you go all the way back, you can see the first commit made to this repository by James Ward in 2013.

If you prefer a more visual interface for viewing commit histories, as well as viewing the changes made in each commit, you can use a program called gitk. For windows users, gitk comes bundled with git.

For Mac users

```
brew install git-gui
```

For Linux users

```
sudo apt-get install gitk
```

To use gitk, in a terminal run `gitk` to view the view the current branches history or `gitk --all` to view all repository commit history.

## Clean Your History

We believe that code should always be done with respect to the latest available main. However, the main might progress while you are working. Rebasing is a mechanism to replay a set of commits ontop of another set as if they were there the whole time. This is nice in theory but sometimes we run into merge conflicts because two parts of history have made changes to the same code and git needs you to decide what is good and what is bad. Some of you are very likely about to experience merge conflicts if someone signed their name before you.

Lets fetch before rebasing so we can use the latest main like we said we should. Fetching is similar to pulling but it wont automatically update your branch with any retrieved changes.

```bash
git fetch
```

- git -> Calls the git program
- fetch -> Command to download data from a remote repository

By default, `fetch` will pull all data from the origin remote, however parameters for a specific remote and branch can be specified such as `git fetch <remote> <branch>`

After doing this, the head of main and the point at which your branch splits off will be mismatched. This can be visualised by running `gitk --all`.

Now we can run:

```bash
git rebase origin/main
```

This will place our commits at the head of the origin/main branch, making it seem as if the new main commits were made before we even branched off.

When encountering a merge conflict, the rebase process will pause and tell you where the issue is. Running `git status` will also tell you which files have merge conflicts. To fix the issue, navigate to the conflicting files. In these files there will be two versions of this file, one being current (what is currently on main) and the other being what is incoming (your changes). To resolve this issue, you can simply delete the incoming or current versions or mix and match the versions. Once you are done solving the conflict, the file should look as if it never had the two versions in it, removing all extra funky characters.

Remember our intent when solving the merge conflict. We want to add our name to `names.txt` but not remove anyone elses. Our change should reflect that.

Once we have resolved the merge conflicts, we can restage the file by doing `git add names.txt` and then continue the rebase with `git rebase --continue`.

When editing, you should fetch, rebase and merge your changes frequently to make solving merge conflicts quicker and easier, instead of trying to do it all in one chunk.

## Push Your Code

As of now, all the work you have done is only available locally. It needs to be uploaded before anyone can can review and add your code to the main branch.

To do this we run:
```bash
git push
```

- git -> Exectues the git program
- push -> Puts a copy of your commit history onto the remote repository

By default, git pushes to `<origin>` `<branch_name>`, however `remote` and `branch` parameters can also be used

If it is the first time pushing, git will reject the push as there is currently no branch in the origin remote that matches your local branch, so, we must create one. To create a remote branch, run:

```bash
git push --set-upstream origin <name_of_your_branch>
```

- --set-upstream -> Command to create a remote branch for your branch
- origin -> Parameter, telling it to create a branch in the origin remote
- name_of_your_branch -> Parameter saying to create a branch of a specific name

The terminal will also give you instructions to do this, simply run the command it gives you.

If you need to push again the the future a simple `git push` should suffice.

> [!NOTE]
In order to complete this step, you must have a github account setup and be added to our organisation**

Follow the steps here to create an account: https://docs.github.com/en/get-started/onboarding/getting-started-with-your-github-account

Once done, please ask a team member with admin permissions to add you to the organisation.

## Make a Pull Request

To merge our modified remote branch into the remote main, we create what is called a Pull Request or PR. A PR essentially outlines all commits you have made on the branch and allows others to view, make suggestions and approve the changes. Once approved, the PR can be merged into the main branch.

When pushing your changes for the first time, git will automatically generate a pull request for you to submit, simply click the link in the terminal and follow the directions in the webpage. Once a pull request is created for your branch, you can continue adding to it by using `git push`.

If it is not the first push, you can manually create a PR by going to the repository on github -> pull requests -> new pr. Make sure you set the correct base branch and target branch.

Once you have created a PR, let someone know by requesting their review through github, messaging them on slack or sending them an email. People should often be checking both their email and slack, however, slack is often the faster method of communication.

## Cleaning up

Once your branch has been merged into main, you can prepare your local main for a new feature. First, run `git checkout main` to switch back to the main branch. Run a `git pull` to get the most up to date version from the remote repo.

Now, you can delete your local editing branch by running

```bash
git branch -d <your_branch_name>
```

- git -> Executes the git program
- branch -> Command to list, create or delete branches
- -d -> Parameter to delete a branch
- your_branch_name -> Parameter teeling the command what branch to delete 

## That's it

Congratulations! you have successfully cloned, branched, modified, merged and pushed your first bit of Drop Bears code.

Welcome To The Software Team

## Further reading

[The definitive book guide for git!](http://git-scm.com/book)

## Suggestions

Feel free to edit this, and make a pull request if you think it could be better! ;)


## Contributors

- AB 04 Dec 24
- LM 03 Dec 24
- JRW 02 Nov 13
