# Install Supervisor on AWS EC2 (Ubuntu)

## 📌 Overview

**Supervisor** is a process control system for Linux that allows you to monitor and manage long-running processes.

In Laravel applications, Supervisor is commonly used to keep the **queue worker** running continuously. If the queue worker crashes or the server reboots, Supervisor automatically restarts it.

### Real-Life Example

Imagine you have an E-commerce application.

When a customer places an order, Laravel pushes several tasks into the queue:

- Send Order Confirmation Email
- Send SMS Notification
- Update Inventory
- Generate Invoice
- Push Notification

Without Supervisor:

```
Customer Order
      │
      ▼
Queue Worker Stops ❌
      │
Jobs Remain Pending
```

With Supervisor:

```
Customer Order
      │
      ▼
Laravel Queue
      │
      ▼
Supervisor
      │
      ▼
Queue Worker Running 24/7 ✅
```

---

# Step 1 — Update System

```bash
sudo apt update
```

---

# Step 2 — Install Supervisor

```bash
sudo apt install supervisor -y
```

---

# Step 3 — Verify Installation

Check Supervisor version.

```bash
supervisord --version
```

Example Output:

```text
4.2.5
```

---

# Step 4 — Enable Supervisor

Enable Supervisor to start automatically after reboot.

```bash
sudo systemctl enable supervisor
```

---

# Step 5 — Start Supervisor

```bash
sudo systemctl start supervisor
```

---

# Step 6 — Check Supervisor Status

```bash
sudo systemctl status supervisor
```

Expected Output:

```text
Active: active (running)
```

You can also use:

```bash
sudo service supervisor status
```

---

# Step 7 — Check Supervisor Process

```bash
ps aux | grep supervisord
```

Example Output

```text
root      1234  0.0  supervisord
```

---

# Step 8 — Check if Supervisor Starts Automatically

```bash
systemctl is-enabled supervisor
```

Expected Output

```text
enabled
```

---

# Supervisor Configuration Directory

Supervisor configuration files are stored in:

```text
/etc/supervisor/
```

Main configuration file:

```text
/etc/supervisor/supervisord.conf
```

Laravel worker configuration files:

```text
/etc/supervisor/conf.d/
```

Example:

```text
/etc/supervisor/conf.d/laravel-worker.conf
```

---

# Useful Supervisor Commands

## Restart Supervisor

```bash
sudo systemctl restart supervisor
```

---

## Stop Supervisor

```bash
sudo systemctl stop supervisor
```

---

## Start Supervisor

```bash
sudo systemctl start supervisor
```

---

## Reload Configuration

```bash
sudo supervisorctl reread
```

---

## Update Configuration

```bash
sudo supervisorctl update
```

---

## Check Status

```bash
sudo supervisorctl status
```

---

## Restart All Processes

```bash
sudo supervisorctl restart all
```

---

## Stop All Processes

```bash
sudo supervisorctl stop all
```

---

## Start All Processes

```bash
sudo supervisorctl start all
```

---

# Why We Use Supervisor

| Feature            | Benefit                                  |
| ------------------ | ---------------------------------------- |
| Auto Restart       | Automatically restarts crashed processes |
| Auto Start         | Starts processes after server reboot     |
| Process Monitoring | Monitors long-running processes          |
| Logging            | Keeps logs for debugging                 |
| Multiple Programs  | Can manage multiple background services  |

---

# Common Use Cases

- Laravel Queue Workers
- Laravel Horizon
- Node.js Applications
- Python Scripts
- WebSocket Servers
- Scheduled Background Jobs
- Long Running PHP Scripts

---

# Best Practices

- Always enable Supervisor on production servers.
- Keep worker configuration files inside `/etc/supervisor/conf.d/`.
- Use dedicated log files for each process.
- Monitor Supervisor status regularly.
- Restart Supervisor after configuration changes.
