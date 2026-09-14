# Linux Fundamentals

## Terminal & Help Commands

```text
| Command          | Description                                                     |
| ---------------- | --------------------------------------------------------------- |
|   pwd            | Displays the current working directory.                         |
|   whoami         | Shows the currently logged-in user.                             |
|   id             | Displays user ID, group ID, and group information.              |
|   hostname       | Displays the system hostname.                                   |
|   hostnamectl    | Displays or changes hostname and system information.            |
|   date           | Displays the current date and time.                             |
|   cal            | Displays a calendar.                                            |
|   clear          | Clears the terminal screen.                                     |
|   history        | Displays previously executed commands.                          |
|   man command    | Opens the detailed manual page for a command.                   |
|   command --help | Displays basic usage and available options.                     |
|   whatis command | Shows a short description of a command.                         |
|   which command  | Shows the location of a command's executable.                   |
|   type command   | Shows whether a command is a binary, alias, shell builtin, etc. |
|   alias          | Creates or displays command shortcuts.                          |
|   unalias        | Removes an existing alias.                                      |
```

## File & Directory Management

```text
| Command                 | Description                                                                    |
| ----------------------- | ------------------------------------------------------------------------------ |
|   ls                    | Lists files and directories.                                                   |
|   ls -l                 | Displays detailed file information such as permissions, owner, size, and date. |
|   ls -la                | Displays detailed information including hidden files.                          |
|   cd directory          | Changes to the specified directory.                                            |
|   cd ..                 | Moves to the parent directory.                                                 |
|   cd ~                  | Moves to the current user's home directory.                                    |
|   cd -                  | Returns to the previous directory.                                             |
|   mkdir dir             | Creates a new directory.                                                       |
|   mkdir -p a/b/c        | Creates nested directories, including missing parent directories.              |
|   touch file            | Creates an empty file or updates its timestamp.                                |
|   cp file destination   | Copies a file.                                                                 |
|   cp -r dir destination | Recursively copies a directory.                                                |
|   mv file destination   | Moves or renames a file/directory.                                             |
|   rm file               | Removes a file.                                                                |
|   rm -r dir             | Recursively removes a directory and its contents.                              |
|   rm -rf dir            | Forcefully removes a directory without confirmation; use with extreme caution. |
|   rmdir dir             | Removes an empty directory.                                                    |
|   file filename         | Identifies the actual type of a file.                                          |
|   stat file             | Displays detailed file metadata, permissions, ownership, and timestamps.       |
|   tree                  | Displays directory structure in a tree format.                                 |
```

## File Reading & Text Processing

```text
| Command            | Description                                                       |
| ------------------ | ----------------------------------------------------------------- |
|   cat file         | Displays the complete contents of a file.                         |
|   less file        | Reads large files page by page.                                   |
|   more file        | Displays file contents page by page.                              |
|   head file        | Displays the first lines of a file.                               |
|   head -n 20 file  | Displays the first 20 lines.                                      |
|   tail file        | Displays the last lines of a file.                                |
|   tail -n 50 file  | Displays the last 50 lines.                                       |
|   tail -f file     | Continuously displays new lines added to a file; useful for logs. |
|   nl file          | Displays file contents with line numbers.                         |
|   wc file          | Counts lines, words, and bytes.                                   |
|   wc -l file       | Counts the number of lines in a file.                             |
|   sort file        | Sorts lines of text.                                              |
|   uniq file        | Removes consecutive duplicate lines.                              |
|   cut              | Extracts specific fields or columns from text.                    |
|   tr               | Translates, replaces, or removes characters.                      |
|   tee file         | Displays output on screen and writes it to a file simultaneously. |
|   diff file1 file2 | Compares two files and displays their differences.                |
|   cmp file1 file2  | Performs a byte-by-byte comparison of two files.                  |
```

## Search Commands

```text
| Command                     | Description                                                 |
| --------------------------- | ----------------------------------------------------------- |
|   find /path -name file     | Searches for files by name.                                 |
|   find /path -type f        | Searches for regular files.                                 |
|   find /path -type d        | Searches for directories.                                   |
|   find /path -size +100M    | Finds files larger than 100 MB.                             |
|   find /path -mtime -7      | Finds files modified within the last 7 days.                |
|   find /path -user username | Finds files owned by a specific user.                       |
|   locate filename           | Quickly searches for files using a database.                |
|   updatedb                  | Updates the database used by `locate`.                      |
|   grep "text" file          | Searches for specific text inside a file.                   |
|   grep -i                   | Performs a case-insensitive search.                         |
|   grep -r "text" /path      | Recursively searches directories for text.                  |
|   grep -n                   | Displays matching line numbers.                             |
|   grep -v                   | Displays lines that do not match the pattern.               |
|   grep -E                   | Uses extended regular expressions for searching.            |
|   xargs                     | Converts command output into arguments for another command. |

```
