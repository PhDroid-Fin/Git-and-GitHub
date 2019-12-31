# Basic commands for Git and GitHub

## Basics
### Core concepts: 3 areas of a Git repository
  * Working Tree: current working space where we edit our files
  * Staging Area (Index): create snapshots of files of which the changes we want to document. Only the changes in the staging area are put in the next commit
  * History: document all the commit history, kept in a hidden file `.git`

### Command line
  * Make directory: `mkdir <directory>`
  * Change directory: `cd <directory>`
  * Open files using atom: `atom <filename>`
  * List the files in the current directory: `ls`
  * Copy files: `cp <filename> <new filename>`
  * Create files: `touch <filename.suffix>`
  * Show content of the file: `cat <filename>`

### Configure Git username and email
  * Configure username: `git config --global user.name "PhDroid-Fin"`
  * Configure email: `git config --global user.email "howard.hao.ma@gmail.com"`
  * Show username and email: `git config --list`
  * In case need different usernames:     
    * `git config --local user.email "your@email.com"`
    * `git config --local user.name "alias"`

### Use Git to track changes
  * Initialization: `git init`
  * Current status: `git status `. (Show any untracked/uncommitted changes)
  * Add files to the staging area (track the files): `git add <filename>/ S* (files with the same prefix 'S') /*.txt(all files with txt suffix) / . (all files)`
    * This will create a unique SHA-1 hash with the first 7 characters shown below the command
  * Add new commits to the history: `git commit -m "your message"
`
  * Show the commit graph information: `git log `
  * Show the difference of the tracked file between the working tree and the staging area: `git diff`. (what we are about to stage)
  * Show the difference of the tracked file between the staging area and the history: `git diff --staged`. (what we are about to commit)
  * Remove tracked files from both the working tree and the staging area: `git rm <filename>`
  * Show the commit message file: `git commit`
    * Use `Ctrl + c`, then type `:wq` to exit.

### Use Git to undo your commands
  * Undo changes in the working tree: `git checkout -- <filename>`
  * Undo staging of files: `git reset HEAD <filename>`
  * Get back the deleted files using `git rm`:
    * Check the log: `git log -- <filename>`
    * Recover the deleted file to both the working tree and the staging area: `git checkout <first 5 characters behind 'commit'> -- <filename>`

### Ignore files unwanted for tracking
  * Open ignore file: `atom/vi(Ctrl+c, type :wq to exit) .gitignore`
  * Type in unwanted file names or directories (using wildcards): `*.suffix`, `logs/` (all files under directory `logs`)

## Branching and Merging
### Branching
  * HEAD: it is a HEAD pointer showing us which branch we are in, but not the commit; or it tells us which branch we have checked out
  * Show a nice labeled commit path: `git log --all --decorate --oneline --graph`
  * Define a shortcut for the above command: `alias <shortcut name>="<the long command>"`. e.g. `alias graph="git log --all --decorate --oneline --graph"`
  * Create new branches: `git branch <branch name>`
  * Check all branches: `git branch`
  * Checkout and work on branches: `git checkout <branch  name>`
  * Stage and commit at the same time: `git commit -a -m "<message>"`
### "Fast-forward" merge
  * Merge master with branch1
    * master --> branch1
  * Show differences between two branches: `git diff <branch1>..<branch2>`
  * Move HEAD to the branch we want to update 'branch1': `git checkout <branch1>`
  * Merge the current branch 'branch1' with 'branch2': `git merge <branch2>`. This will move 'master' branch to where <branch name> is.
  * Show merged branches: `git branch --merged`
### 3-way merge (recursive strategy)
  * Merge branch1 with branch 2:
    * master --> branch1;
    * master --> branch2;
    * The two branches changed different lines!!!
### Deleting branches
  * Delete branches that have been merged: `git branch -d <branch name>`
### Merge conflicts
  * This occurs when we try to merge two branches that changed the same lines
  * Checkout and move to a new branch: `git checkout -b <branch name>`
  * Abort the merge due to conflicts: `git merge --abort`
  * Explanation on the conflicts:
    * `<<<< HEAD`: HEAD pointer's content
    * `====`: equal sign showing content in comparison
    * `>>>> <branch>`: content in another branch
  * Solution:
    * delete `<<<< HEAD`, unwanted content and `>>>> <branch>`.
    * Then delete the branch with conflicts

### Detached HEAD
  * Usually HEAD points to a branch which in turns points to a commit
  * When the HEAD points to a commit in the history, it is called a detached HEAD
    * Find the commit: `git log` to see the commit hash
    * Point to the commit: `git checkout <7 character>`
    * Check the HEAD: `graph`
    * Quit the detached HEAD: `git checkout <branch name>`
    * Create a new branch from the detached HEAD: `git branch <new Branching>`

### Git stash
  * When switching to another branch but don't want to commit the changes in the staging area.
  * For example,  you want to checkout to another branch before make the commit. But you don't want to lose it.
  * `git checkout <branch name>` return message "error: Your local changes to the following files would be overwritten by checkout. Please commit your changes or stash them before you switch branches."
  * Solution: use `git stash` to store the changes in staging area for a moment.
  * When you come back, use `git stash list` to show the unsaved commits in time order (most recent with lowest number)
  * `git stash list -p` to show the details
  * Apply: `git stash apply`
  * Apply and remove: `git stash pop`
  * Add stash with a  message: `git stash save "<message>"`
  * Remove stash: `git stash drop <stash_id>`; Remove all `git stash clear`

## Git - Remotes (GitHub)
### Overview
  * Download: Git Fetch and merge
  * Upload: Git Push
  * GitHub is a remote repository
### Commands
  * Origin: `origin` works as an alias by default
  * Retrieve a copy repo from GitHub (Clone): `git clone <the address copied from the repo>`
  * Setup the usernames: `git config --local user.name "<username>"`; `git config --local user.email "<email>"`
  * Display our remotes: `git remote`: usually it's 'origin' by default
  * Display full locations of our remotes: `git remote -v`
  * Display how master branch looks at origin: `graph`; (HEAD -> master, origin/master) tells us our local repo is in sync with our remote named origin
  * Check out remote (detached HEAD): `git checkout origin/master`
  * Update our origin: `git fetch origin`
  * When the origin is ahead of our local repo: `git merge origin/<branch name>`
  * Do git fetch and merge together: `git pull` (not recommended)
  * Upload local repo to the origin: `git push`
