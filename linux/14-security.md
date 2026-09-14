# Security

## Firewall

```text
| Command               | Description                        |
| --------------------- | ---------------------------------- |
|   ufw status          | Displays firewall status.          |
|   ufw enable          | Enables UFW firewall.              |
|   ufw disable         | Disables UFW firewall.             |
|   ufw allow 22        | Allows SSH traffic on port 22.     |
|   ufw allow 80        | Allows HTTP traffic on port 80.    |
|   ufw allow 443       | Allows HTTPS traffic on port 443.  |
|   ufw deny 23         | Blocks port 23.                    |
|   ufw delete allow 80 | Removes an existing firewall rule. |

Firewalld
----------
firewall-cmd --state
firewall-cmd --list-all
firewall-cmd --get-active-zones
firewall-cmd --add-service=http
firewall-cmd --add-service=https
firewall-cmd --permanent --add-service=http
firewall-cmd --reload
```

## Security & Authentication

```text
| Command           | Description                                     |
| ----------------- | ----------------------------------------------- |
|   sudo            | Executes commands with elevated privileges.     |
|   visudo          | Safely edits the `/etc/sudoers` configuration.  |
|   passwd          | Changes a user's password.                      |
|   chage           | Manages password expiration policies.           |
|   last            | Displays login history.                         |
|   lastlog         | Displays the last login information for users.  |
|   who             | Displays currently logged-in users.             |
|   w               | Displays logged-in users and their activities.  |
|   fail2ban-client | Manages and checks Fail2Ban status and actions. |
|   ssh-keygen      | Generates secure SSH authentication keys.       |

```
