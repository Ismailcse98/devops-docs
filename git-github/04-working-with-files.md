# Working with Files

## Add Specific File
Stages a specific file so its current changes can be included in the next commit.
```bash
git add index.php
```

## Add Multiple Files
Stages multiple specified files at once.
```bash
git add file1.php file2.php
```

## Add All Changes
Stages new, modified, and deleted files within the current directory.
```bash
git add .
```

## Add All Repository Changes
Stages all changes throughout the repository, including files outside the current directory.
```bash
git add -A
```

## Interactive Staging
Allows you to interactively select individual changes/hunks to stage.
```bash
git add -p
```

## Unstage File
Removes a file from the staging area without deleting its working-directory changes.
```bash
git restore --staged file.php
```

## Unstage All Files
Removes all staged changes while keeping the modifications in your working directory.
```bash
git restore --staged .
```
