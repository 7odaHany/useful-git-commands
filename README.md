
# Useful Git Commands



## Table of contents

* [Setting up git](#setting-up-git)
* [Initializing a repository in an existing directory](#initializing-a-repository-in-an-existing-directory)
* [Checking the status of your files](#checking-the-status-of-your-files)
* [Staging files](#staging-files)
* [Committing files](#committing-files)
* [Branching and merging](#branching-and-merging)
* [Resetting](#resetting)
* [Git remote](#git-remote)
* [Git blame](#git-blame)
* [Git log](#git-log)
* [Checking what you are committing](#checking-what-you-are-committing)
* [Useful Commands](#useful-commands)
* [Useful Alias](#useful-alias)
* [Contributing](#contributing)

#### Git

Git is a distributed version control system used to track changes in files and coordinate work on those files among multiple people.

##### Setting up git

Set your Git configuration:

```sh
$ git config --global user.name "Your Name"
$ git config --global user.email "your.email@example.com"
```

##### Initializing a repository in an existing directory

To start tracking an existing project in Git:

```sh
$ git init
```
This creates a .git subdirectory to track the files in your project. To start tracking files, add them to the staging area and commit:

```sh
$ git add <file>
$ git commit -m 'Initial commit'
```

#### Checking the status of your files

Check the current status of your repository:

```sh
$ git status
```
This shows which files are staged, unstaged, or untracked.

#### Staging files

To stage files for the next commit:

```sh
# Add a specific file
$ git add filename

# Add all files
$ git add -A

# Add all changes in the current directory
$ git add .

# Interactively add changes
$ git add -p
```

#### Stashing files

If you need to save changes without committing them, stash them:

```sh
# Stash changes
$ git stash

# Stash changes with a custom message
$ git stash save "message"

# Reapply the latest stash
$ git stash apply

# Drop a specific stash
$ git stash drop stash@{0}

# Apply and remove a stash
$ git stash pop

# List all stashes
$ git stash list

# Show the latest stash changes
$ git stash show

# See diff details of a given stash number
$ git diff stash@{0}
```

#### Committing files

Once files are staged, commit them:

```sh
# Commit staged changes
$ git commit -m "commit message"

# Add and commit in one step
$ git commit -am "commit message"

# Amend the previous commit
$ git commit --amend

# Squashing commits together
$ git rebase -i
This will give you an interface on your core editor:
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell

# Squashing commits together using reset --soft
$ git reset --soft HEAD~number_of_commits
$ git commit
** WARNING: this will require force pushing commits, which is OK if this is on a branch before you push to master or create a Pull Request.
```

#### Branching and merging

Create and switch between branches:

```sh
# Create a new branch
$ git checkout -b branchname  or $ git switch -c branchname

# Switch between branches
$ git checkout - or $ git switch branchname

# Pushing local branch to remote
$ git push -u origin branchname

# Deleting a local branch - this won't let you delete a branch that hasn't been merged yet
$ git branch -d branchname

# Deleting a local branch - this WILL delete a branch even if it hasn't been merged yet!
$ git branch -D branchname

# Remove any remote refs you have locally that have been removed from your remote (you can substitute <origin> to any remote branch)
$ git remote prune origin

# Viewing all branches, including local and remote branches
$ git branch -a

# Viewing all branches that have been merged into your current branch, including local and remote
$ git branch -a --merged

# Viewing all branches that haven't been merged into your current branch, including local and remote
$ git branch -a --no-merged

# Viewing local branches
$ git branch

# Viewing remote branches
$ git branch -r

# Rebase master branch into local branch
$ git rebase origin/master

# Pushing local branch after rebasing master into local branch
$ git push origin +branchname
```

#### Fetching and checking out remote branches

Fetch and work with remote branches:

```sh
# This will fetch all the remote branches for you.
$ git fetch origin

# Checkout a remote branch locally
$ git checkout -b test origin/test

# Deleting a remote branch
$ git branch -rd origin/branchname
$ git push origin --delete branchname  or  $ git push origin:branchname
```

#### Merging branch to trunk/master

To merge a branch into master:

```sh
# First checkout trunk/master
$ git checkout trunk/master

# Now merge branch to trunk/master
$ git merge branchname

# To cancel a merge
$ git merge --abort
```

#### Updating a local repository with changes from a Github repository

To update your local repository with the latest changes from the remote:

```sh
$ git pull origin master
```

#### Tracking existing branch

To set up a local branch to track a remote branch:

```sh
$ git branch --set-upstream-to=origin/branchname branchname
```

#### Resetting

Reset your working directory or history:

```sh
# Soft reset (keep changes in working directory)
$ git reset --soft [commit]

# Hard reset (discard all changes)
$ git reset --hard

# Reset specific file to the latest commit
$ git reset HEAD -- filename
```

#### Git remote

Manage remote repositories:

```sh
# Show where 'origin' is pointing to and also tracked branches
$ git remote show origin

# Show where 'origin' is pointing to
$ git remote -v

# Change the 'origin' remote's URL
$ git remote set-url origin https://github.com/user/repo.git
```

#### Git blame

See who made changes to a file:

```sh
# Show alteration history of a file with the name of the author
$ git blame filename

# Show author and commit SHA
$ git blame [filename] -l
```

#### Git log

View commit history:

```sh
# Show commit log
$ git log

# List of commits showing commit messages and changes
$ git log -p

# List of commits with the particular expression you are looking for
$ git log -S 'something'

# List of commits by author
$ git log --author 'Author Name'

# Show summary of commits
$ git log --oneline

# Shows log by author and searching for specific term inside the commit message
$ git log --grep "term" --author "name"
```

#### Checking what you are committing

Review changes before committing:

```sh
# See all (unstaged) changes done to a local repo
$ git diff

# See all (staged) changes done to a local repo
$ git diff --cached

# Compare with the remote
$ git diff --stat origin/master
```

#### Useful commands

```sh
# Check if a commit is tagged
$ git tag --contains [sha]

# Number of commits by author
$ git shortlog -s --author 'Author Name'

# showing the number of commits per author, sorted by the number of commits in descending order
$ git shortlog -s -n

# List of commit comments by author & the total number of commits this the author
$ git shortlog -n --author 'Author Name'

# Undo local changes to a File
$ git checkout -- filename

# Shows more detailed info about a commit
$ git cat-file [sha] -p

#  Show a list of trached files
$ git ls-files

# Count lines added/removed by an author
$ git log --author="Author Name" --pretty=tformat: --numstat --since=month | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "Added: %s, Removed: %s, Total: %s\n", add, subs, loc }'
```

### Contributing

1. Fork the repository.
2. Create a new branch: `git checkout -b my-new-feature`.
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push -u origin my-new-feature`
5. Submit a pull request 
