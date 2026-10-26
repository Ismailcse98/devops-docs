# Branch Management

## Create Branch
Creates a new branch without switching to it.
```bash
git branch feature/login
```

## Switch Branch
Switches the working directory to an existing branch.
```bash
git switch feature/login
```

## Create and Switch Branch
Creates a new branch and immediately switches to it.
```bash
git switch -c feature/login
```

## Older Checkout Method
Switches to an existing branch; git switch is generally clearer for branch switching.
```bash
git checkout feature/login
```

## Create Branch with Checkout
Creates and switches to a new branch.
```bash
git checkout -b feature/login
```

## Rename Current Branch
Renames the currently checked-out branch.
```bash
git branch -m new-name
```

## Delete Local Branch
Deletes a local branch when Git determines it has been safely merged.
```bash
git branch -d feature/login
```

## Force Delete Local Branch
Forcefully deletes a local branch even if it contains unmerged changes.
```bash
git branch -D feature/login
```





