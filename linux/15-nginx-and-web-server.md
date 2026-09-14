# Nginx & Web Server

## Nginx Administration

```text
| Command                   | Description                                                    |
| ------------------------- | -------------------------------------------------------------- |
|   nginx -t                | Tests Nginx configuration syntax.                              |
|   nginx -T                | Displays the complete active Nginx configuration.              |
|   systemctl status nginx  | Checks Nginx service status.                                   |
|   systemctl start nginx   | Starts Nginx.                                                  |
|   systemctl stop nginx    | Stops Nginx.                                                   |
|   systemctl restart nginx | Restarts Nginx.                                                |
|   systemctl reload nginx  | Reloads Nginx configuration with minimal service interruption. |
|   curl localhost          | Tests the local web server.                                    |
|   ss -tulnp \| grep :80   | Identifies the process listening on port 80.                   |

```
