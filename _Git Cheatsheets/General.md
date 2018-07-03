# General Commands

Notes I took from watching CS50's guide to Git. Will add to later once I start to learn how to use Git more and better.

## `git clone <url>`

Copies an online repository to local storage.

## `git add <file1> <file2> <file3> ... <fileN>`

Adds an element to the staging area. Use `git add .` to add everything in the current directory, as well as all
sub-directories.

## `git diff`

Displays the differences between the version of the repo hosted on your computer and the version hosted on GitHub.

## `git commit`

Commits the changes you've made. Using this command will automatically put you in the message creation mode. Use
`git commit -m "<Your message in quotation marks>"` to add the message as you commit.

## `git status`

Display the status of the git project, displaying items in the staging area, untracked items, and modified items.

## `git push`

Send a committed version of a repo online to GitHub. The version I've been using most often is
`git push -u origin master`, though I'm pretty sure those last two keywords will change depending on what branch I'm
working with.

## `git log`

Displays all commits made to the current repo.

## `git reset`

Lets you roll back to an earlier version off the repo. Use `git reset --hard <version ID>` to reset to a specific
version. Use `git reset --hard origin/master` to reset your current branch back to the current origin master.

This command also lets you undo additions to the staging area. You just need to use
`git reset HEAD -- <file or directory name>`.

## `git branch`

Displays all branches within the current repo.

## `git branch <new branch name>`

Creates a new branch with the indicated name.

## `git merge <source branch>`

Merges the source branch into the current branch. **This can cause merge conflicts!**
