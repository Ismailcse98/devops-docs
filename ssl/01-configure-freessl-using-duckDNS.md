# Configure Free SSL (Let's Encrypt) on AWS EC2 Using DuckDNS

This guide explains how to configure a free HTTPS SSL certificate on an AWS EC2 Ubuntu Server using DuckDNS, Nginx, and Let's Encrypt (Certbot).


---

## Prerequisites

    - AWS EC2 Instance
    - Ubuntu Server
    - Public IPv4 Address
    - Security Group allows:
        - TCP 22 (SSH)
        - TCP 80 (HTTP)
        - TCP 443 (HTTPS)
    - Nginx Installed

---

## Step 1: Create a Free Domain

```text
Visit: https://www.duckdns.org

Login with your GitHub, Google, Reddit, or X account.

Create a subdomain.

Example: laravel-devops

Your free domain will be: laravel-devops.duckdns.org

Update the IP Address with your EC2 Public IPv4.

Example: x.xxx.xxx.xxx

Verify DNS propagation:

ping laravel-devops.duckdns.org

or

nslookup laravel-devops.duckdns.org

Expected: x.xxx.xxx.xxx

```

## Step 2: Install Nginx

```bash
sudo apt update 
sudo apt install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx
sudo systemctl status nginx
```

## Step 3: Create Nginx Virtual Host

Create a configuration file:

```bash
sudo nano /etc/nginx/sites-available/laravel-devops
```

Example configuration:
```bash
server { 
    listen 80; 
    server_name laravel-devops.duckdns.org; 
    root /var/www/html; 
    index index.html; 
    location / { try_files $uri $uri/ =404; } 
}
```

Enable the site:
```bash
sudo ln -s /etc/nginx/sites-available/laravel-devops /etc/nginx/sites-enabled/
```

Remove the default site (recommended):
```bash
sudo rm -f /etc/nginx/sites-enabled/default
```

Test configuration:
```bash
sudo nginx -t
```

Reload Nginx:
```bash
sudo systemctl reload nginx
```

## Step 4: Create a Test Page
```bash
echo "<h1>HTTPS Setup Successful</h1>" | sudo tee /var/www/html/index.html
```
Visit: http://laravel-devops.duckdns.org

## Step 5: Install Certbot
```bash
sudo apt install certbot python3-certbot-nginx -y
```
Verify installation:
```bash
certbot --version
```

## Step 6: Generate SSL Certificate
Generate the certificate for your DuckDNS domain:
```bash
sudo certbot --nginx -d laravel-devops.duckdns.org
```

## Step 7: Verify SSL
Open:
```bash
https://laravel-devops.duckdns.org
```

Expected result:
    - HTTPS enabled
    - Browser security lock icon
    - Automatic HTTP → HTTPS redirect

## Step 8: Verify Installed Certificates
```bash
sudo certbot certificates
```

## Step 9: Test Automatic Renewal
```bash
sudo certbot renew --dry-run
```
Check renewal timer:
```bash
systemctl list-timers | grep certbot
```

## Common Issues
**403 Forbidden**

Possible causes:

    - index.html not found
    - Incorrect root path
    - Permission issues
    - Wrong Laravel public directory

## Check Nginx Error Logs
```bash
sudo tail -50 /var/log/nginx/error.log
```
# Conclusion
For production environments, use a custom domain purchased from a domain registrar and follow the same SSL configuration process.
