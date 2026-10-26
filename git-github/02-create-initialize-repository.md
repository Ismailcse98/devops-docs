# Create & Initialize Repository

## Initialize Repository
Creates a new Git repository in the current directory by creating a .git directory.
```bash
git init
```

## Initialize Repository with Main Branch
Creates a new Git repository and immediately sets main as its initial branch.
```bash
git init -b main
```

## Clone Repository
Downloads an existing Git repository, including its history, branches, and files.
```bash
git clone https://github.com/user/project.git
```

## Clone into Custom Directory
Clones the repository into a directory with your chosen name.
```bash
git clone https://github.com/user/project.git my-project
```

## Clone Specific Branch
Clones the repository and checks out the specified branch.
```bash
git clone -b develop https://github.com/user/project.git
```

## Clone without Full History
Creates a shallow clone containing only the latest commit, useful for CI/CD and faster downloads.
```bash
git clone --depth 1 https://github.com/user/project.git
```