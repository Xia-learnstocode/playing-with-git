# Git Cheatsheet

## Initialise Local Directory as Git Directory

- Initialise present working directory: `git init`

## Add files

- Add a specific file: `git add <file-name>`
- Add all files in current directory: `git add .`

## Commit files with a commit message:

- `git commit -m "commit message here"`

## Check Status

- `git status`

## Git VIM Editor

Add merge message:

1. press "i" (i for insert)
2. write your merge message
3. press "esc" (escape)
4. write ":wq" (write & quit)
5. then press enter

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

### Check Branches

- See local branches: `git branch`
- See remote branches: `git branch -r.`

## Git Merge

- Merge branches: `git merge <branch-name>`

## Git Rebase

Rebase is a way to integrate changes from one branch to another as if they happened sequentially even if they happened on 2 separate branches in parallel.

- Rebase into this branch: `git rebase <branch-name>`

### Interactive Rebasing

**Allows you to re-order & select the commits you want to include**

Using the rebase command with the -i option.

Git will open up a UI to show you which commits are about to be copied below the target of the rebase. It also shows their commit hashes and messages, which is great for getting a bearing on what's what.

For Git in Terminal, the UI window means opening up a file in a text editor like vim.

You can do many more things like squashing (combining) commits, amending commit messages, and even editing the commits themselves.

`git rebase -i <commit-name>`

e.g. `git rebase-i HEAD~4` will move your current location back by 4 commits & open an UI window that allows you to select & reorder the commits you want to include.

## Detaching HEAD

HEAD refers to the current branch you are viewing.
When HEAD points to a commit that is not the last commit in a branch, that is a "detached HEAD"

- Detach the HEAD at a certain commit: `git checkout <commit-hash>`

## Relative Refs

### Moving upwards one commit at a time: `^`

- `git <commit-name>^` allows you to move upwards to the first parent of the commit
- `git <commit-name>^^` allows you to move upwards to the first **grandparent** of the commit
- You can also use `<commit-hash>` instead of `<commit-name>`

### Moving upwards a number of times: `~<num>`

The tilde operator (optionally) takes in a trailing number that specifies the number of parents you would like to ascend.
This is a way to concisely refer to a commit

- `git <commit-name>~<num>

#### Branch Forcing

Branch forcing combined with relative refs allows you to quickly moved a branch to the location of a commit.

- Directly reassign a branch to a commit with the -f option: `git branch -f <branch-you-want-to-move> <commit-you-want-to-move-it-to>`
  e.g. Move (by force) the main branch to three parents behind HEAD: `git branch -f main HEAD~3`

## Reversing Changes in Git

- For local branches: reverse changes by moving a branch reference backwards in time to an older commit: `git reset`
  This will move a branch backwards as if the commit had never been made in the first place.
  e.g. `git reset HEAD~1`
- `for remote branches: reverse changes and share those reversed changes with others: `git revert`.
- e.g.`git revert HEAD`

## Moving Work Around

### Cherry Picking

- Copy a series of commits below your current location (HEAD): `git cherry-pick <Commit1> <Commit2> <...>`
