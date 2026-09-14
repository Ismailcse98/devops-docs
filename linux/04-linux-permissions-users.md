# Linux Permissions & Users

## Permission Commands

```text
| Command                 | Description                                                           |
| ----------------------- | --------------------------------------------------------------------- |
|   ls -l                 | Displays file and directory permissions.                              |
|   chmod 755 file        | Gives the owner full permission and others read/execute permission.   |
|   chmod 644 file        | Gives the owner read/write permission and others read permission.     |
|   chmod +x script.sh    | Adds execute permission to a file.                                    |
|   chmod -x script.sh    | Removes execute permission.                                           |
|   chown user file       | Changes the file owner.                                               |
|   chown user:group file | Changes both owner and group.                                         |
|   chgrp group file      | Changes the group ownership.                                          |
|   umask                 | Controls default permissions for newly created files and directories. |
|   getfacl file          | Displays Access Control List (ACL) permissions.                       |
|   setfacl               | Sets advanced ACL permissions for users and groups.                   |
```

## User & Group Management
```text
| Command                  | Description                                            |
| ------------------------ | ------------------------------------------------------ |
|   useradd username       | Creates a new user.                                    |
|   adduser username       | Interactively creates a new user.                      |
|   passwd username        | Sets or changes a user's password.                     |
|   usermod                | Modifies an existing user's configuration.             |
|   usermod -aG group user | Adds a user to an additional group.                    |
|   userdel username       | Deletes a user.                                        |
|   userdel -r username    | Deletes a user and their home directory.               |
|   groupadd group         | Creates a new group.                                   |
|   groupdel group         | Deletes a group.                                       |
|   groups username        | Displays the groups a user belongs to.                 |
|   gpasswd                | Manages group membership and group passwords.          |
|   su - username          | Switches to another user.                              |
|   sudo command           | Executes a command with elevated privileges.           |
|   sudo -i                | Opens a root login shell.                              |
|   who                    | Displays currently logged-in users.                    |
|   w                      | Displays logged-in users and their current activities. |
|   last                   | Displays login history.                                |
```


