# Git Cheatsheet

## Initialise Local Directory as Git Directory

- Initialise present working directory: `git init`

## Add files

- Add a specific file: `git add <file-name>
- Add all files in current directory: `git add .`

## Commit files with a commit message:

- `git commit -m "commit message here"`

## Check Status

- `git status`

## Remote

- Check remote: `git remote -v`
- Add remote: `git remote origin <remote-url>`
- Change remote: `git remote set-url <remote-name> <remote-url>`
  e.g. `git remote set-url origin <remote-url>`
- Remove remote:

## Push files to GitHub:

- Pushing for the 1st time: `git push -u origin main`
- Pushing after the 1st time: `git push`

## Pull files from Github

- Pushing for the 1st time: `git pull -u origin main`
- Pushing after the 1st time: `git pull`

## Git Branching

- Create branch: `git branch <branch-name>`
- Switch branch: `Git checkout <branch-name>`
- Create branch & checkout branch `git checkout -b <branch-name>`
- Delete branch: `git branch -d <branch-name>`
- Confirm delete if branch has unmerged commits: `git branch -D <branch-name>`
-

## Git Merge

- Merge branches: `git merge <branch-name>`

## Git Rebase

- Rebase into this branch: `git rebase <branch-name>`

## Detaching HEAD

HEAD refers to the current branch you are viewing.
When HEAD points to a commit that is not the last commit in a branch, that is a "detached HEAD"

- Detach the HEAD at a certain commit: `git checkout <commit-hash>`
