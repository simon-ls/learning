# Git

## General

- rigin = remote repo
- The HEAD only points to one commit, the one that the working tree stat currently corresponds to
- Newly created commits are called _heads_

## Index

- The _index_ is a cache for preparing a commit
- If you have staged some file changes and later modified the working tree file again, you can use the **Discard** command to either revert the working tree file content to the staged changes stored in the Index, or to the file content stored in the repository (HEAD).

## Commits

- Every commit (except the init) has a parent. Merges can have multiple.

## Braches

- The default local branch created by Git is named _master._ The master tracks the remote branch origin/master
- Cloning a remote repository clones all its local branches, which are then stored in your local repository as remote branches.
- You can&#39;t work directly on remote branches, but have to create local branches, which are linked to the remote branches
- Branches are just pointers to commits

## Merge

- If a commit cannot be performed e.g. if there was conflicts. There are 2 ways to finish merge:
  - resolve the conflicts, stage changes, and commit to working tree
  - reverting the whole working tree

## Commands

- **Checkout:** Moves the HEAD
- **Merge: **
  - Normal: has at least two parent commits, new commit is created
  - Fast-forward Merge: No extra commits are created, the pointer is just moved forward
  - Squash merge: like a normal merge, but branch commits information is discarded
- **Rebase:** Alternative to merging is rebasing. This will keep the history linear by moving a branch from one commit to another. It is done by _recreating your work of once branch onto another_.
- **Cherry-Pick:** Apply certain commits from another branch, to the current



## Example Workflow

### New Branch
1. git chekout master
2. git pull --all
3. git checkout -b feature/....
4. git commit ....
5. git push (https://help.github.com/articles/pushing-to-a-remote/)

### Merge branch in
1. git checkout [parent]
2. git pull --all
3. git merge [child]
4. gulp and resolve
5. git push
6. repeat for epic and dev/staging
