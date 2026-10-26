# Fetch, Pull & Push

## Fetch Remote Changes
Downloads new commits and references from the remote without modifying your working branch.
```bash
git fetch origin
```

## Fetch All Remotes
Fetches updates from all configured remote repositories.
```bash
git fetch --all
```

## Fetch and Prune
Fetches remote updates and removes stale remote-tracking branches that no longer exist remotely.
```bash
git fetch --prune
```

## Pull Changes
Fetches remote changes and integrates them into the current branch.
```bash
git pull
```

## Pull with Rebase
Fetches remote changes and replays your local commits on top of them instead of creating a merge commit.
```bash
git pull --rebase
```

## Push Branch
Uploads the specified local branch and its commits to the remote repository.
```bash
git push origin feature/login
```

## Push Current Branch
Pushes the current branch to its configured upstream branch.
```bash
git push
```

## Set Upstream Branch
Pushes the branch and establishes its remote upstream relationship.
```bash
git push -u origin feature/login
```

## Push All Branches
Pushes all local branches to the specified remote.
```bash
git push --all origin
```

## Push Tags
Uploads all local Git tags to the remote repository.
```bash
git push --tags
```


