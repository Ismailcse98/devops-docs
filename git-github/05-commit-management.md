# Commit Management

## Create Commit
Creates a commit containing the currently staged changes.
```bash
git commit -m "Add user authentication"
```

## Commit All Tracked Changes
Stages and commits modifications/deletions to already tracked files; it does not include new untracked files.
```bash
git commit -am "Fix login validation"
```

## Create Empty Commit
Creates a commit without file changes, useful for triggering CI/CD pipelines.
```bash
git commit --allow-empty -m "Trigger deployment"
```

## Amend Last Commit
Modifies the most recent commit, commonly used to change its message or add forgotten staged changes.
```bash
git commit --amend
```

## Amend Commit Message
Replaces the message of the most recent commit.
```bash
git commit --amend -m "Updated commit message"
```

## Show Commit History
Displays each commit in a compact single-line format.
```bash
git log --oneline
```

## Graph History
Displays branches, merges, tags, and commits as a visual ASCII graph.
```bash
git log --oneline --graph --decorate --all
```

