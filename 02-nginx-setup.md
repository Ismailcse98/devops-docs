# Nginx Installation and Configuration Guide


## Step 1: Connect to the Server

SSH into your server.

```bash
ssh -i MyKeyPair.pem ubuntu@<PUBLIC_IP>
```

Verify the connection:

```bash
whoami
```

Expected output:

```text
ubuntu
```

---

## Step 2: Update the System

Update the package index before installing new software.

```bash
sudo apt update
```

(Optional) Upgrade installed packages.

```bash
sudo apt upgrade -y
```

---

## Step 3: Install Nginx

Install Nginx using the APT package manager.

```bash
sudo apt install nginx -y
```

Verify the installation.

```bash
nginx -v
```

Example output:

```text
nginx version: nginx/1.24.0
```

---

## Step 4: Start the Nginx Service

Start the Nginx service.

```bash
sudo systemctl start nginx
```

Enable Nginx to start automatically after a reboot.

```bash
sudo systemctl enable nginx
```

Check the service status.

```bash
sudo systemctl status nginx
```

Expected status:

```text
Active: active (running)
```

Exit the status screen by pressing `q`.

---

## Step 5: Configure the Firewall

If UFW is enabled, allow HTTP and HTTPS traffic.

```bash
sudo ufw allow 'Nginx Full'
```

Verify the firewall rules.

```bash
sudo ufw status
```

---

## Step 6: Allow Traffic in AWS Security Group

If your server is running on Amazon EC2, ensure the following inbound rules are configured:

| Type | Port | Source |
|------|------|--------|
| HTTP | 80 | Anywhere (0.0.0.0/0) |
| HTTPS | 443 | Anywhere (0.0.0.0/0) |

---

## Step 7: Verify Nginx

Open your browser and visit:

```text
http://<PUBLIC_IP>
```

You should see the **Welcome to Nginx!** page.

---

## Step 8: Nginx Directory Structure

Common Nginx directories:

| Path | Description |
|------|-------------|
| `/etc/nginx/` | Main configuration directory |
| `/etc/nginx/nginx.conf` | Main configuration file |
| `/etc/nginx/sites-available/` | Available site configurations |
| `/etc/nginx/sites-enabled/` | Enabled site configurations |
| `/var/www/html/` | Default website root |
| `/var/log/nginx/` | Nginx log files |

---

## Step 9: Create a Simple Website

Navigate to the default web directory.

```bash
cd /var/www/html
```

Create or edit the default page.

```bash
sudo nano index.html
```

Example:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Nginx Server</title>
</head>
<body>
    <h1>Welcome to Nginx!</h1>
    <p>Your web server is running successfully.</p>
</body>
</html>
```

Save and exit.

---

## Step 10: Test the Configuration

Before restarting Nginx, verify the configuration.

```bash
sudo nginx -t
```

Expected output:

```text
syntax is ok
test is successful
```

---

## Step 11: Reload Nginx

Apply configuration changes without interrupting active connections.

```bash
sudo systemctl reload nginx
```

Or restart the service.

```bash
sudo systemctl restart nginx
```

---

## Common Nginx Commands

Start Nginx:

```bash
sudo systemctl start nginx
```

Stop Nginx:

```bash
sudo systemctl stop nginx
```

Restart Nginx:

```bash
sudo systemctl restart nginx
```

Reload Configuration:

```bash
sudo systemctl reload nginx
```

Check Status:

```bash
sudo systemctl status nginx
```

Enable on Boot:

```bash
sudo systemctl enable nginx
```

Disable on Boot:

```bash
sudo systemctl disable nginx
```

---

## View Log Files

Access log:

```bash
sudo tail -f /var/log/nginx/access.log
```

Error log:

```bash
sudo tail -f /var/log/nginx/error.log
```

---

## Troubleshooting

### Nginx service won't start

Check the service status.

```bash
sudo systemctl status nginx
```

Review the error logs.

```bash
sudo journalctl -xeu nginx
```

---

### Configuration errors

Test the configuration.

```bash
sudo nginx -t
```

---

### Website not loading

Verify:

- Nginx service is running.
- Security Group allows ports **80** and **443**.
- UFW (if enabled) allows HTTP/HTTPS traffic.
- DNS records (if using a domain) point to the correct server.

---

## Uninstall Nginx

Remove the package.

```bash
sudo apt remove nginx -y
```

Remove configuration files.

```bash
sudo apt purge nginx -y
```

Remove unused dependencies.

```bash
sudo apt autoremove -y
```