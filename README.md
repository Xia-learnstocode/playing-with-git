# Git Cheatsheet

## Setup

### Initialise Local Directory as Git Directory

- Initialise present working directory: `git init`

## Committing

### Add files

- Add a specific file: `git add <file-name>`
- Add all files in current directory: `git add .`

### Commit files with a commit message:

- `git commit -m "commit message here"`

### Check Status

- Check the status of the files in your git directory (added, staged or commited): `git status`

### Git Log

- Show a list of all comits made to a repository: `git log`, `git log --pretty=oneline`
- View branches: `git log --pretty=oneline --graph`
- Search commit messages: `git log --grep='pattern' --pretty=oneline`
- Show file history: `git log --pretty=oneline -- <file-name>`
- Show directory history: `git log --pretty=oneline --all -- <dir>`
- Show last 5 commits: `git log --pretty=oneline -5`

## Pushing & Pulling Files to GitHub

### Remote

- Add remote: `git remote origin <remote-url>`
- Check remote: `git remote -v`
- Change remote: `git remote set-url <remote-name> <remote-url>`
  e.g. `git remote set-url origin <remote-url>`
- Remove remote: `git remote remove origin`

### Push files to GitHub:

- Pushing for the 1st time: `git push -u origin main`
- Pushing after the 1st time: `git push`

### Pull files from Github

- Pushing for the 1st time: `git pull -u origin main`
- Pushing after the 1st time: `git pull`

## Branching

### Git Branching

- Create branch: `git branch <branch-name>`
- Switch branch: `Git checkout <branch-name>`
- Create branch & checkout branch `git checkout -b <branch-name>`
- Delete branch: `git branch -d <branch-name>`
- Confirm delete if branch has unmerged commits: `git branch -D <branch-name>`

### Check Branches

- See local branches: `git branch`
- See remote branches: `git branch -r.`
- See all local & remote branches: `git branch -a`

### Diff

- Show modifications not yet staged: `git diff`
- Show modifications not yet commited: `git diff --staged`
- Show all changes since last commi: `git diff HEAD`
- Show all changes since a spwecific (tagged) commit: `git diff v1.0 -- <file-name>`
- Show differecnes between 2 tagged commits: `git diff v1.0 v1.1 --stat`

### Git Merge

- Merge branches: `git merge <branch-name>`

### Detaching HEAD

HEAD refers to the current branch you are viewing.
When HEAD points to a commit that is not the last commit in a branch, that is a "detached HEAD"

- Detach the HEAD at a certain commit: `git checkout <commit-hash>`

### Git VIM Editor

Add merge message:

1. press "i" (i for insert)
2. write your merge message
3. press "esc" (escape)
4. write ":wq" (write & quit)
5. then press enter

## Relative Refs

### Moving Up By One Commit

- Moving upwards one commit at a time: `^`
- Move upwards to the first parent of the commit: `git <commit-name>^`
- Move upwards to the first **grandparent** of the commit: `git <commit-name>^^`
- You can also use `<commit-hash>` instead of `<commit-name>`

### Moving Up By Multiple Commits

The tilde operator `~` (optionally) takes in a trailing number that specifies the number of parents you would like to ascend.
This is a way to concisely refer to a commit

- Moving upwards a number of times: `git <commit-name>~<num>`

### Branch Forcing

Branch forcing combined with relative refs allows you to quickly moved a branch to the location of a commit.

- Directly reassign a branch to a commit with the -f option: `git branch -f <branch-you-want-to-move> <commit-you-want-to-move-it-to>`
  e.g. Move (by force) the main branch to three parents behind HEAD: `git branch -f main HEAD~3`

### Reversing Changes in Git

- For local branches: reverse changes by moving a branch reference backwards in time to an older commit: `git reset`
  This will move a branch backwards as if the commit had never been made in the first place.
  e.g. `git reset HEAD~1`
- For remote branches: reverse changes and share those reversed changes with others: `git revert`
- e.g.`git revert HEAD`
- Unstage a file: `git reset HEAD <file-name>`
- Create an alias for unstaging a file:

```git
git config --global alias.unstage 'reset HEAD'
$ git unstage <file-name>
```

- Discard changes to a file: `git checkout -- <file>`
- Rollback to a specific commit:
  1. Make a note of the SHAR for the commit that you want to rollback to
  2. Switch to the branch and reset the head to the required commit

```git
git log --pretty=oneline
git branch mybranch
$ git reset --hard <SHAR>
```

- Overwrite remote commit history with local history: `git push --force`

## Moving Work Around

### Cherry Picking

- Copy a series of commits below your current location (HEAD): `git cherry-pick <Commit1> <Commit2> <...>`

Cherry-pick will plop down a commit from anywhere in the tree onto HEAD (as long as that commit isn't an ancestor of HEAD).

### Rebasing

Rebase is a way to integrate changes from one branch to another as if they happened sequentially even if they happened on 2 separate branches in parallel.

- Rebase into this branch: `git rebase <branch-name>`

#### Interactive Rebasing

**Allows you to re-order & select the commits you want to include**

Using the rebase command with the -i option.

Git will open up a UI to show you which commits are about to be copied below the target of the rebase. It also shows their commit hashes and messages, which is great for getting a bearing on what's what.

For Git in Terminal, the UI window means opening up a file in a text editor like vim.

You can do many more things like squashing (combining) commits, amending commit messages, and even editing the commits themselves.

`git rebase -i <commit-name>`

e.g. `git rebase-i HEAD~4` will move your current location back by 4 commits & open an UI window that allows you to select & reorder the commits you want to include.

## Making Changes to a Commit

Modify the most recent commit & edit the previous commit message without changing its snapshot: `git commit --amend`

This command combines staged changes with the previous commit instead of creating an entirely new commit. It replaces the most recent commit with a new commit with its own ref.

e.g.
`git commit --amend -m "an update commit message"`

![Initial History](https://wac-cdn.atlassian.com/dam/jcr:34fd0826-9e89-4ef1-bce8-b1325cf48306/01-02%20Changing%20the%20Last%20Commit.svg?cdnVersion=40)

## Setting Anchor Points

### Git Tags

(Somewhat) permanently marks certain commits as "milestones" so that you can reference then like a branch.

Tags never move as more commits are created. You can't "check out" a tag and then complete work on that tag -- tags exist as **anchors** in the commit tree that designate certain spots.

Add a tag to a commit: `git tag <tag-name> <commit-name-or-hash>`

You go into detached HEAD state when you checkout a commit with a tag - this is because you can't commit directly onto the v1 tag.

e.g.
Making a tag at C1 which is our version 1 prototype: `git tag v1 c1`

If you leave the commit off, git will just use whatever HEAD is at.

#### Git Describe

Describe where you are relative to the closest "anchor" (aka tag):

```
git describe <ref>
```

Where `<ref>` is anything git can resolve into a commit. If you don't specify a ref, git just uses where you're checked out right now (`HEAD`).

e.g.
`git describe main` or ` git describe <branch-name>` or `git describe <commit-nmae-or-hash>`

The output of the command looks like:

`<tag>_<numCommits>_g<hash>`

Where `tag` is the closest ancestor tag in history, `numCommits` is how many commits away that tag is, and `<hash>` is the hash of the commit being described.

Git describe can help you get your bearings after you've moved many commits backwards or forwards in history; this can happen after you've completed a git bisect (a debugging search) or when sitting down at a coworkers computer who just got back from vacation.

# Resources

1. [Learn Git Branching](https://learngitbranching.js.org)
2. [Atlassian Git Tutorials](https://www.atlassian.com/git)
