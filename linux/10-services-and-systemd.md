# Services & systemd

## Systemctl
```text
| Command                               | Description                                            |
| ------------------------------------- | ------------------------------------------------------ |
|   systemctl status nginx              | Displays the current status of a service.              |
|   systemctl start nginx               | Starts a service.                                      |
|   systemctl stop nginx                | Stops a service.                                       |
|   systemctl restart nginx             | Restarts a service.                                    |
|   systemctl reload nginx              | Reloads service configuration without a full restart.  |
|   systemctl enable nginx              | Configures a service to start automatically at boot.   |
|   systemctl disable nginx             | Disables automatic startup at boot.                    |
|   systemctl is-active nginx           | Checks whether a service is currently active.          |
|   systemctl is-enabled nginx          | Checks whether a service starts automatically at boot. |
|   systemctl list-units                | Lists loaded systemd units.                            |
|   systemctl list-units --type=service | Lists systemd services.                                |
|   systemctl daemon-reload             | Reloads systemd configuration after unit file changes. |

```