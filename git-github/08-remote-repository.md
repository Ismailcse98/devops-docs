# Remote Repository

## Add Remote
Connects your local repository to a remote repository named origin.
```bash
git remote add origin https://github.com/user/project.git
```

## Show Remote
Displays the URLs configured for fetching and pushing.
```bash
git remote -v
```

## Rename Remote
Changes the name of an existing remote repository.
```bash
git remote rename origin upstream
```

## Change Remote URL
Changes the URL used by a remote repository.
```bash
git remote set-url origin https://github.com/user/new-project.git
```

## Remove Remote
Removes a remote repository configuration from the local repository.
```bash
git remote remove origin
```

## Show Remote Details
Displays detailed information about the remote, including branches and tracking information.
```bash
git remote show origin
```
