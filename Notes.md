# Notes

## If you're on Windows use Git BASH
https://git-for-windows.github.io/


## Show status
```
git status
```


## Stash changes
```
git stash
```

## Tracking a new branch ('There is no tracking information for the current branch.')
```
git branch --set-upstream-to=origin/<remote> <local>
```

## Undoing stuff
- Discard all local changes
```
git reset --hard HEAD
```
- Discard local changes in a specific file (or multiple files)
```
git checkout HEAD <file> [<file2> ...]
```
- Revert a pushed commit (creates a new commit)
```
git revert <commit>
```
- Reset the latest commit pointer (HEAD) to a previous commit **discarding all changes**
```
git reset --hard <commit>
```
- Reset the latest commit pointer (HEAD) to a previous commit **preserving all changes as *unstaged* changes**
```
git reset <commit>
```
- Reset the latest commit pointer (HEAD) to a previous commit **preserving all changes as *uncommitted* changes**
```
git reset --keep <commit>
```
- Undo last commit
```
git commit -m 'Something terribly misguided'
git reset HEAD~
<< edit files as necessary >>
git add .
git commit -c ORIG_HEAD
```
- Undo 'git add'
```
git reset <file>
```

### Reset options
~~~~
--soft: Just move HEAD, keep changes
--mixed: As above but also unstage changes
--hard: As above but also modify local working directory
~~~~

## How do I force 'git pull' to overwrite local files?
```
git fetch --all
git reset --hard origin/<branch_name>
```

## How to modify existing, unpushed commits?
```
git commit --amend
git push <remote> <branch> --force
```

## Moving existing, uncommited work to a new branch in Git
```
git checkout -b <new-branch>
git add <files>
git commit
```

## Ignore files that have already been committed to a Git repository
```
git rm -r --cached .
git add .
git commit -m '.gitignore is now working'
```

or alternatively:

```
git reset <file>
echo filename >> .gitignore
```

## Cleaning up local commits interactively before pushing
```
git rebase --interactive
git rebase --interactive origin branch
```

## Avoid repeated merge conflicts (using the 'reuse recorded resolution' feature)
```
git config --global rerere.enabled true
```

## Incomplete merges: You have not concluded your merge (MERGE_HEAD exists)
```
git merge --abort # Undo merge
git add .
git commit -m 'Undone merge'
git pull
git push
```

or alternatively:

```
git reset –-merge ORIG_HEAD
git add .
git commit -m 'Undone merge'
git pull
git push
```

## Get changes from upstream in forked repository
```
git pull upstream
```

## Pull and merge with minimal conflicts
```
git pull --rebase
```

## Rewrite the history of a branch if all else fails (WARNING: Handle with extreme care!)
```
git filter-branch --force --index-filter \
'git rm --cached --ignore-unmatch <PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA>' \
--prune-empty --tag-name-filter cat -- --all
git push origin --force --all
git push origin --force --tags
```

**Prune and remove garbage from index**
```
git for-each-ref --format='delete %(refname)' refs/original | git update-ref --stdin
git reflog expire --expire=now --all
git gc --prune=now
```

## Cheat sheets
- https://about.gitlab.com/images/press/git-cheat-sheet.pdf
- https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf

## See also
- http://gitref.org/basic/
- http://ibrokegit.com/
- merging and rebasing: https://www.atlassian.com/git/tutorials/merging-vs-rebasing
- ORIG_HEAD: http://stackoverflow.com/questions/17595524/orig-head-fetch-head-merge-head-etc
- carets and tildes: http://www.paulboxley.com/blog/2011/06/git-caret-and-tilde
