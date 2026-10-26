# Merge

## Merge Branch
Merges the specified branch into the currently checked-out branch.
```bash
git merge feature/login
```

## No Fast-Forward Merge
Creates an explicit merge commit even when Git could perform a fast-forward merge.
```bash
git merge --no-ff feature/login
```

## Abort Merge
Cancels an in-progress merge and attempts to restore the repository to its previous state.
```bash
git merge --abort
```

## Continue Merge
Continues a merge after conflicts have been resolved and staged.
```bash
git merge --continue
```





