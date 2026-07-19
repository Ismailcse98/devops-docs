# Install Composer on AWS EC2 (Ubuntu)

This guide explains how to install the latest version of **Composer** on an Ubuntu-based AWS EC2 instance.


## Step 1: Download the Composer Installer

```bash
curl -sS https://getcomposer.org/installer -o composer-setup.php
```

---

## Step 2: Verify the Installer (Optional)

Retrieve the latest installer signature and verify the installer.

```bash
HASH=$(curl -sS https://composer.github.io/installer.sig)

php -r "if (hash_file('sha384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
```

---

## Step 3: Install Composer Globally

```bash
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

---

## Step 4: Remove the Installer

```bash
rm composer-setup.php
```

---

## Step 5: Verify the Installation

Check the installed Composer version.

```bash
composer --version
```

Example output:

```text
Composer version 2.x.x
```

---

## Update Composer

To update Composer to the latest version:

```bash
sudo composer self-update
```

---

## Useful Commands

### Check Composer Version

```bash
composer --version
```

### Display Composer Help

```bash
composer
```

### Check Composer Diagnostics

```bash
composer diagnose
```