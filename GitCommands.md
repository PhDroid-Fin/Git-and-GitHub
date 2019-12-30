# Basic commands for Git and GitHub

## Git
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

### Configure Git username and email
  * Configure username: `git config --global user.name "PhDroid-Fin"`
  * Configure email: `git config --global user.email "howard.hao.ma@gmail.com"`
  * Show username and email: `git config --list`
  * In case need different usernames:     
    * `git config --local user.email "your@email.com"`
    * `git config --local user.name "alias"`

### Git commands
  * Initialization: `git init`
  * Statuses of both the working tree and (most importantly) the staging area: `git status `. (Any changes to the tracked files, and any untracked files that are newly created)
  * Add files to the staging area (track the files): `git add <filename>/ S* (files with the same prefix 'S') /*.txt(all files with txt suffix) / . (all files)`
    * This will create a unique SHA-1 hash with the first 7 characters shown below the command
  * Add new commits to the history: `git commit -m "your message"
`
  * Show the commit graph information: `git log `
  * Show the difference of the tracked file between the working tree and the staging area: `git diff`. (what we are about to stage)
  * Show the difference of the tracked file between the staging area and the history: `git diff --staged`. (what we are about to commit)
