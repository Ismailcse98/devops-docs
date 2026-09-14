# Linux Logs

## Log Management

```text
| Command                      | Description                            |
| ---------------------------- | -------------------------------------- |
|   journalctl                 | Displays systemd journal logs.         |
|   journalctl -u nginx        | Displays logs for a specific service.  |
|   journalctl -f              | Continuously follows system logs.      |
|   journalctl -b              | Displays logs from the current boot.   |
|   journalctl -p err          | Displays error-level logs.             |
|   journalctl --since today   | Displays today's logs.                 |
|   dmesg                      | Displays kernel messages.              |
|   tail -f /var/log/syslog    | Continuously monitors syslog.          |
|   tail -f /var/log/auth.log  | Monitors authentication-related logs.  |
|   grep ERROR application.log | Searches application logs for `ERROR`. |

```
