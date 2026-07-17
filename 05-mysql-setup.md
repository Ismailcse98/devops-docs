# Install MySQL Server on Ubuntu

## Update Package Index

```bash
sudo apt update
sudo apt upgrade -y
```

---

## Install MySQL

```bash
sudo apt install mysql-server -y
```

---

## Verify Installation

```bash
mysql --version
```

Example

```
mysql Ver 8.0.xx
```

---

## Check Service

```bash
sudo systemctl status mysql
```

---

## Enable Auto Start

```bash
sudo systemctl enable mysql
```

---

## Start MySQL

```bash
sudo systemctl start mysql
```

---

## Restart MySQL

```bash
sudo systemctl restart mysql
```

---

## Stop MySQL

```bash
sudo systemctl stop mysql
```

---

## Check Listening Port

```bash
sudo ss -tulpn | grep 3306
```

Expected

```
127.0.0.1:3306
```

Never expose port **3306** publicly unless absolutely required.

# Secure MySQL

Run

```bash
sudo mysql_secure_installation
```

The installer will ask several questions.

---

## Validate Password Component

```
Would you like to setup VALIDATE PASSWORD component?
```

Recommendation

```
Y
```

---

## Password Policy

Choose

```
2
```

Strong Password

Example

```
Minimum Length : 8

Contains

Uppercase

Lowercase

Number

Special Character
```

---

## Remove Anonymous Users

```
Remove anonymous users?
```

Choose

```
Y
```

Anonymous users should never exist in production.

---

## Disable Remote Root Login

```
Disallow root login remotely?
```

Choose

```
Y
```

Never allow root login remotely.

---

## Remove Test Database

```
Remove test database?
```

Choose

```
Y
```

---

## Reload Privileges

```
Reload privilege tables now?
```

Choose

```
Y
```

# Login

```bash
sudo mysql
```

or

```bash
mysql -u root -p
```

Exit

```sql
exit;
```

# Create Database

```sql
CREATE DATABASE laravel_app
CHARACTER SET utf8mb4
COLLATE utf8mb4_unicode_ci;
```

Verify

```sql
SHOW DATABASES;
```

# Create Database User

```sql
CREATE USER 'laravel_user'@'localhost'
IDENTIFIED BY 'StrongPassword123!';
```

Grant Permissions

```sql
GRANT ALL PRIVILEGES
ON laravel_app.*
TO 'laravel_user'@'localhost';
```

Reload

```sql
FLUSH PRIVILEGES;
```

Verify

```sql
SHOW GRANTS FOR 'laravel_user'@'localhost';
```

Never use **root** for Laravel applications.

```bash
mysql -u laravel_user -p
```

Select Database

```sql
USE laravel_app;
```

Show Tables

```sql
SHOW TABLES;
```

# .env

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel_app
DB_USERNAME=laravel_user
DB_PASSWORD=StrongPassword123!
```

Run

```bash
php artisan migrate
```

Never expose MySQL publicly.

Good

```
3306 → Private Network Only
```

Bad

```
0.0.0.0/0
```

If using AWS EC2

Security Group

```
Inbound

3306

Source

Private EC2 Security Group
```

NOT

```
0.0.0.0/0
```

# Backup

```bash
mysqldump -u root -p laravel_app > backup.sql
```

Compressed Backup

```bash
mysqldump -u root -p laravel_app | gzip > backup.sql.gz
```

# Restore

```bash
mysql -u root -p laravel_app < backup.sql
```

Compressed

```bash
gunzip < backup.sql.gz | mysql -u root -p laravel_app
```

Check Version

```bash
mysql --version
```

Check Status

```bash
sudo systemctl status mysql
```

Restart

```bash
sudo systemctl restart mysql
```

Logs

```bash
sudo journalctl -u mysql
```

Configuration

```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

## Can't Login

```bash
sudo systemctl status mysql
```

---

## Reset Root Password

```bash
sudo systemctl stop mysql
sudo mysqld_safe --skip-grant-tables &
mysql
```

---

## Port Already in Use

```bash
sudo lsof -i :3306
```

---

## Check Error Logs

```bash
sudo journalctl -u mysql
```

Ubuntu Log

```bash
sudo tail -100 /var/log/mysql/error.log
```
