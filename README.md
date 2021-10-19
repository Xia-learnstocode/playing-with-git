# Git Commands

## Initialise Local Directory as Git Directory

`git init`

## Add files

- Add a specific file: `git add <file-name>
- Add all files in current directory: `git add .`

## Commit files with a commit message:

- `git commit -m "commit message here"`

## Check Status

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

- Switch branch: `Git checkout <branch-name>`
- Delete branch: `git branch -d <branch-name>`
- Confirm delete if branch has unmerged commits: `git branch -D <branch-name>`
