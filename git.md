# Git
* Graphical view of branches `git log --all --graph --decorate --oneline --simplify-by-decoration`

## Stash
### List stashed commits
```
git stash list
```

### Show changes in the last stashed commit
```
git stash show -p
```

### Show changes in an arbitrary conmit
```
# where n is the commit you want to target from the stash list
git stash show stash@{n} -p 
```
