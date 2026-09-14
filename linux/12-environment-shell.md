# Environment & Shell

## Environment Variables

```text
| Command                     | Description                                                 |
| --------------------------- | ----------------------------------------------------------- |
|   env                       | Displays environment variables.                             |
|   printenv                  | Displays environment variables.                             |
|   echo $PATH                | Displays the current `PATH` variable.                       |
|   export APP_ENV=production | Sets an environment variable for the current shell/session. |
|   unset APP_ENV             | Removes an environment variable.                            |
|   source .env               | Loads variables from a file into the current shell.         |
|   set                       | Displays shell variables and functions.                     |

```

## Bash & Command Control

```text
| Command                  | Description                                                      |
| ------------------------ | ---------------------------------------------------------------- |
|   echo "Hello"           | Prints text or command output to the terminal.                   |
|   read name              | Reads input from the user.                                       |
|   command1 && command2   | Executes the second command only if the first succeeds.          |
|   command1 \|\| command2 | Executes the second command if the first fails.                  |
|   command1 ; command2    | Executes both commands regardless of the first command's result. |
|   command > file         | Redirects standard output to a file and overwrites it.           |
|   command >> file        | Appends standard output to a file.                               |
|   command 2> error.log   | Redirects error output to a file.                                |
|   command &              | Runs a command in the background.                                |
|   command \| grep text   | Sends command output to another command through a pipe.          |
|   $(command)             | Uses command output inside another command.                      |
|   chmod +x script.sh     | Makes a shell script executable.                                 |
|   bash script.sh         | Executes a Bash script.                                          |
|   sh script.sh           | Executes a script using the POSIX shell.                         |

```
