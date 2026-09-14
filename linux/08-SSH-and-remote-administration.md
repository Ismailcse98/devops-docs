# SSH & Remote Administration

## SSH Commands

```text
| Command                        | Description                                                   |
| ------------------------------ | ------------------------------------------------------------- |
|   ssh user@server              | Connects to a remote Linux server.                            |
|   ssh -p 2222 user@server      | Connects using a custom SSH port.                             |
|   ssh-keygen                   | Generates an SSH key pair.                                    |
|   ssh-copy-id user@server      | Copies the public key to the remote server.                   |
|   scp file user@server:/path   | Copies a file to a remote server over SSH.                    |
|   scp user@server:/path/file . | Downloads a file from a remote server.                        |
|   rsync                        | Efficiently synchronizes files between systems.               |
|   rsync -avz                   | Synchronizes files using archive mode and compression.        |
|   ssh -L                       | Creates local port forwarding.                                |
|   ssh -R                       | Creates remote port forwarding.                               |
|   ssh -N                       | Creates an SSH connection without executing a remote command. |

```