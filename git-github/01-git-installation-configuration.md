## Git Installation & Configuration

### Check Git Version:-

Checks the installed Git version and confirms whether Git is available on your system.
```bash
git --version
```

### Set Global Username:-

Sets the author name that Git uses for commits across all repositories.
```bash
git config --global user.name "Your Name"
```

### Set Global Email:-

Sets the email associated with your Git commits.
```bash
git config --global user.email "you@example.com"
```

### View Git Configuration:-

Displays the Git configuration currently applied to your environment.
```bash
git config --list
```

### View Global Configuration:-

Shows only your global Git configuration settings.
```bash
git config --global --list
```

### Get a Specific Configuration:-

Displays the currently configured Git username.
```bash
git config user.name
```

### Set Default Branch Name:-

Configures newly initialized repositories to use main as the default branch.
```bash
git config --global init.defaultBranch main
```

### Set Git Editor:-

Sets VS Code as Git's default editor for commit messages and other operations.
```bash
git config --global core.editor "code --wait"
```

### Remove Configuration:-

Removes a specific global Git configuration value.
```bash
git config --global --unset user.name
```
