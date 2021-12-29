# Git Cheatsheet

## Rebase current branch on top of default branch without checking out

```bash
DEFAULT_BRANCH=$(git symbolic-ref refs/remotes/origin/HEAD | sed 's@^refs/remotes/origin/@@')
```


```bash
git fetch origin $DEFAULT_BRANCH:$DEFAULT_BRANCH
git rebase $DEFAULT_BRANCH
```
