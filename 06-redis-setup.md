# 🚀 Install Redis on AWS EC2 (Ubuntu 24.04 / 22.04)

> Redis is an open-source, in-memory data store used for caching, session management, queues, pub/sub messaging, and high-performance applications. Laravel uses Redis for Cache, Queue, Session, Rate Limiting, and Horizon.

---

# 📋 Prerequisites

Before installing Redis, ensure the following software is already installed:

- ✅ AWS EC2 Ubuntu Server
- ✅ Nginx
- ✅ PHP 8.2
- ✅ Composer
- ✅ MySQL
- ✅ Laravel (Optional)

---

# Step 1 — Update System

Update your package index before installing Redis.

```bash
sudo apt update
sudo apt upgrade -y
```

---

# Step 2 — Install Redis Server

Install Redis from the Ubuntu repository.

```bash
sudo apt install redis-server -y
```

---

# Step 3 — Verify Installation

Check the installed version.

```bash
redis-server --version
```

Example

```text
Redis server v=7.x.x
```

---

# Step 4 — Check Redis Service Status

Verify that Redis is running.

```bash
sudo systemctl status redis-server
```

Expected Output

```text
Active: active (running)
```

Press

```
q
```

to exit.

---

# Step 5 — Enable Redis on Boot

Automatically start Redis after every server reboot.

```bash
sudo systemctl enable redis-server
```

Verify

```bash
sudo systemctl is-enabled redis-server
```

Expected Output

```text
enabled
```

---

# Step 6 — Start / Stop / Restart Redis

Start

```bash
sudo systemctl start redis-server
```

Stop

```bash
sudo systemctl stop redis-server
```

Restart

```bash
sudo systemctl restart redis-server
```

Reload

```bash
sudo systemctl reload redis-server
```

---

# Step 7 — Test Redis

Ping Redis.

```bash
redis-cli ping
```

Expected Output

```text
PONG
```

If you receive `PONG`, Redis is working correctly.

---

# Step 8 — Check Redis Listening Port

Redis listens on port **6379** by default.

```bash
sudo ss -tulpn | grep 6379
```

Expected Output

```text
127.0.0.1:6379
```

Redis should listen only on localhost unless remote access is explicitly required.

---

# Step 9 — Secure Redis Configuration

Open the Redis configuration file.

```bash
sudo nano /etc/redis/redis.conf
```

---

## Bind Address

Ensure Redis is bound to localhost.

```ini
bind 127.0.0.1 ::1
```

Do **NOT** use:

```ini
bind 0.0.0.0
```

unless you fully understand the security implications.

---

## Protected Mode

Ensure protected mode is enabled.

```ini
protected-mode yes
```

---

## Disable Dangerous Commands (Optional)

Rename or disable commands that can destroy data.

```ini
rename-command FLUSHALL ""
rename-command FLUSHDB ""
rename-command CONFIG ""
```

---

## Set a Password

Add a password to require authentication.

```ini
requirepass YourStrongRedisPassword123!
```

Restart Redis after making changes.

```bash
sudo systemctl restart redis-server
```

---

# Step 10 — Test Authentication

Connect to Redis.

```bash
redis-cli
```

Authenticate.

```bash
AUTH YourStrongRedisPassword123!
```

Expected Output

```text
OK
```

Test.

```bash
PING
```

Expected

```text
PONG
```

Exit

```bash
exit
```

---

# Step 11 — Firewall & AWS Security Group

Redis should **never** be exposed to the public Internet.

Good

```
6379 → Private Network Only
```

Bad

```
0.0.0.0/0
```

For AWS Security Groups:

| Port | Source | Recommendation |
|------|--------|----------------|
| 6379 | Private EC2 Security Group | ✅ Allow |
| 6379 | 0.0.0.0/0 | ❌ Never |

---

# Step 12 — Install PHP Redis Extension

Laravel requires the Redis PHP extension.

```bash
sudo apt install php8.2-redis -y
```

Restart PHP-FPM.

```bash
sudo systemctl restart php8.2-fpm
```

Verify.

```bash
php -m | grep redis
```

Expected

```text
redis
```

---

# Step 13 — Install Redis Client (Laravel)

Install the Predis package.

```bash
composer require predis/predis
```

Or use the PHP Redis extension (recommended).

---

# Step 14 — Configure Laravel

Update the `.env` file.

```env
CACHE_STORE=redis
QUEUE_CONNECTION=redis
SESSION_DRIVER=redis

REDIS_CLIENT=phpredis

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=YourStrongRedisPassword123!
REDIS_PORT=6379
```

Clear the configuration cache.

```bash
php artisan optimize:clear
```

---

# Step 15 — Test Laravel Cache

Store data.

```bash
php artisan tinker
```

```php
Cache::put('name', 'Laravel Redis', 600);
```

Retrieve data.

```php
Cache::get('name');
```

Expected

```php
"Laravel Redis"
```

---

# Step 16 — View Redis Information

General information.

```bash
redis-cli INFO
```

Memory usage.

```bash
redis-cli INFO memory
```

Connected clients.

```bash
redis-cli INFO clients
```

Statistics.

```bash
redis-cli INFO stats
```

---

# Step 17 — Monitor Redis

Live monitoring.

```bash
redis-cli monitor
```

Connected clients.

```bash
redis-cli client list
```

---

# Step 18 — Useful Commands

Check Version

```bash
redis-server --version
```

Ping

```bash
redis-cli ping
```

Status

```bash
sudo systemctl status redis-server
```

Restart

```bash
sudo systemctl restart redis-server
```

Configuration File

```bash
sudo nano /etc/redis/redis.conf
```

Logs

```bash
sudo journalctl -u redis-server
```
---

# 🔐 Redis Security Hardening Guide

> Installing Redis is easy. Securing Redis for production is critical.
>
> This guide covers industry-standard Redis security practices for Ubuntu servers running on AWS EC2.

---

# Why Redis Security Matters

Redis is an in-memory database.

By default Redis:

- Has no authentication
- Uses TCP
- Runs on port **6379**
- Can execute destructive commands
- Can be compromised if exposed to the public internet

Never expose Redis directly to the internet.

---

# Security Checklist

- ✅ Bind Redis to localhost
- ✅ Enable Protected Mode
- ✅ Set a Strong Password
- ✅ Disable Dangerous Commands
- ✅ Restrict Port 6379
- ✅ Configure AWS Security Group
- ✅ Keep Redis Updated
- ✅ Use Least Privilege Access

---

# Step 1 — Open Redis Configuration

```bash
sudo nano /etc/redis/redis.conf
```

---

# Step 2 — Bind Redis to Localhost

Find:

```ini
bind 127.0.0.1 ::1
```

This allows only local connections.

Never use:

```ini
bind 0.0.0.0
```

unless Redis is deployed inside a trusted private network.

---

# Step 3 — Enable Protected Mode

Find:

```ini
protected-mode yes
```

If disabled:

```ini
protected-mode no
```

Change it immediately.

Protected mode blocks unauthorized remote access.

---

# Step 4 — Set a Strong Password

Find:

```ini
# requirepass foobared
```

Replace with:

```ini
requirepass MyStrongRedisPassword123!
```

Use a password that contains:

- Uppercase letters
- Lowercase letters
- Numbers
- Special characters
- At least 16 characters

Example:

```
T8!xQ4@rLm9#YvP2
```

Do not use simple passwords such as:

```
redis123
password
123456
admin
```

---

# Step 5 — Disable Dangerous Commands

Some Redis commands can destroy your entire dataset.

Disable them by renaming to an empty string.

```ini
rename-command FLUSHALL ""
rename-command FLUSHDB ""
rename-command CONFIG ""
rename-command DEBUG ""
rename-command SHUTDOWN ""
```

These commands should not be available to application users.

---

# Step 6 — Restart Redis

```bash
sudo systemctl restart redis-server
```

Verify:

```bash
sudo systemctl status redis-server
```

---

# Step 7 — Test Authentication

Connect:

```bash
redis-cli
```

Authenticate:

```bash
AUTH MyStrongRedisPassword123!
```

Expected:

```
OK
```

Test:

```bash
PING
```

Output:

```
PONG
```

Exit:

```bash
exit
```

---

# Step 8 — Verify Listening Address

```bash
sudo ss -tulpn | grep 6379
```

Expected:

```
127.0.0.1:6379
```

Never expose:

```
0.0.0.0:6379
```

---

# Step 9 — AWS Security Group

Allow only trusted servers.

Recommended

| Port | Source |
|------|--------|
|6379|Private EC2 Security Group|

Never

| Port | Source |
|------|--------|
|6379|0.0.0.0/0|

---

# Step 10 — Ubuntu Firewall (UFW)

If UFW is enabled:

Check status:

```bash
sudo ufw status
```

Block Redis port:

```bash
sudo ufw deny 6379
```

Or allow only trusted IPs.

---

# Step 11 — Keep Redis Updated

Update packages regularly.

```bash
sudo apt update
sudo apt upgrade
```

---

# Step 12 — Monitor Failed Access

View Redis logs.

```bash
sudo journalctl -u redis-server
```

Follow logs in real time.

```bash
sudo journalctl -fu redis-server
```

---

# Security Best Practices

✔ Never expose Redis publicly

✔ Use localhost binding

✔ Enable Protected Mode

✔ Configure a strong password

✔ Disable dangerous commands

✔ Restrict AWS Security Groups

✔ Enable firewall protection

✔ Keep Redis updated

✔ Monitor logs regularly

✔ Store passwords in environment variables

✔ Never commit passwords to Git

---

# 🚀 Laravel Redis Integration Guide

> This guide explains how to integrate Redis with Laravel for production environments. Redis improves application performance by handling cache, queues, sessions, rate limiting, and broadcasting efficiently.

---

# Table of Contents

1. Why Redis?
2. Install PHP Redis Extension
3. Verify Installation
4. Redis Client Options
5. Configure Laravel
6. Cache Configuration
7. Queue Configuration
8. Session Configuration
9. Cache Usage
10. Queue Usage
11. Session Usage
12. Testing Redis
13. Horizon (Optional)
14. Production Best Practices
15. Production Checklist

---

# Why Redis?

Laravel uses Redis for:

- Cache
- Queue
- Session
- Rate Limiting
- Broadcasting
- Horizon
- Atomic Locks

Without Redis:

- More database queries
- Slower page loading
- Higher CPU usage
- Increased database load

Redis stores temporary data in memory, making it significantly faster than querying the database repeatedly.

---

# Step 1 — Install PHP Redis Extension

Install the official PHP Redis extension.

```bash
sudo apt update
sudo apt install php8.2-redis -y
```

Restart PHP-FPM.

```bash
sudo systemctl restart php8.2-fpm
```

---

# Step 2 — Verify Installation

Check that the extension is loaded.

```bash
php -m | grep redis
```

Expected Output

```text
redis
```

Or view detailed information.

```bash
php --ri redis
```

---

# Step 3 — Redis Client

Laravel supports two Redis clients.

## PhpRedis (Recommended)

Advantages:

- Native PHP extension
- Faster performance
- Lower memory usage
- Recommended for production

## Predis

Install only if required.

```bash
composer require predis/predis
```

Predis is easier for development but generally slower than PhpRedis.

---

# Step 4 — Configure Environment

Update your `.env` file.

```env
CACHE_STORE=redis
QUEUE_CONNECTION=redis
SESSION_DRIVER=redis

REDIS_CLIENT=phpredis

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=YourStrongRedisPassword123!
REDIS_PORT=6379
```

If no password is configured:

```env
REDIS_PASSWORD=null
```

Never commit real credentials to Git.

---

# Step 5 — Clear Configuration Cache

Apply the new configuration.

```bash
php artisan optimize:clear
```

---

# Step 6 — Cache Configuration

Default configuration (`config/cache.php`):

```php
'default' => env('CACHE_STORE', 'redis'),
```

Store a cache value.

```php
Cache::put('site_name', 'Laravel Redis', now()->addMinutes(10));
```

Retrieve it.

```php
Cache::get('site_name');
```

Delete it.

```php
Cache::forget('site_name');
```

Clear all cache.

```bash
php artisan cache:clear
```

---

# Step 7 — Queue Configuration

Set the queue driver.

```env
QUEUE_CONNECTION=redis
```

Generate a job.

```bash
php artisan make:job SendWelcomeEmail
```

Dispatch the job.

```php
SendWelcomeEmail::dispatch($user);
```

Start the queue worker.

```bash
php artisan queue:work
```

For production, use Supervisor or systemd to keep workers running.

---

# Step 8 — Session Configuration

Store sessions in Redis.

```env
SESSION_DRIVER=redis
```

Benefits:

- Faster sessions
- Shared sessions across multiple servers
- Better scalability

Clear configuration.

```bash
php artisan optimize:clear
```

---

# Step 9 — Rate Limiting

Laravel automatically uses Redis for efficient rate limiting.

Example:

```php
RateLimiter::for('api', function ($request) {
    return Limit::perMinute(60);
});
```

Redis tracks request counts with minimal overhead.

---

# Step 10 — Test Redis Connection

Open Laravel Tinker.

```bash
php artisan tinker
```

Store data.

```php
Cache::put('framework', 'Laravel', 600);
```

Retrieve data.

```php
Cache::get('framework');
```

Expected Output

```php
"Laravel"
```

---

# Step 11 — Verify Redis Keys

Open Redis CLI.

```bash
redis-cli
```

Authenticate if required.

```bash
AUTH YourStrongRedisPassword123!
```

List keys.

```bash
KEYS *
```

You should see Laravel-generated cache or session keys.

> **Note:** Avoid using `KEYS *` in production because it scans the entire keyspace and can impact performance. Prefer `SCAN` for large datasets.

---

# Step 12 — Horizon (Optional)

Install Horizon.

```bash
composer require laravel/horizon
```

Install assets.

```bash
php artisan horizon:install
```

Run migrations.

```bash
php artisan migrate
```

Start Horizon.

```bash
php artisan horizon
```

Access the Horizon dashboard (typically):

```
http://your-domain/horizon
```

Protect the Horizon dashboard using authentication and authorization.

---

# Step 13 — Useful Artisan Commands

Clear application cache.

```bash
php artisan cache:clear
```

Clear configuration cache.

```bash
php artisan config:clear
```

Clear route cache.

```bash
php artisan route:clear
```

Clear view cache.

```bash
php artisan view:clear
```

Optimize application.

```bash
php artisan optimize
```

# 💾 Redis Persistence Guide

> Redis is an in-memory database, but it can also persist data to disk. Persistence protects your data from server restarts, crashes, or unexpected failures. This guide covers Redis persistence strategies and production best practices.

---

# Table of Contents

1. What is Persistence?
2. Why Persistence Matters
3. Redis Persistence Methods
4. RDB (Redis Database Snapshot)
5. AOF (Append Only File)
6. Hybrid Persistence
7. Configure Persistence
8. Verify Persistence
9. Backup Redis Data
10. Restore Redis Data
11. Production Recommendations
12. Best Practices
13. Production Checklist

---

# What is Persistence?

By default, Redis stores data in memory (RAM).

If persistence is **disabled**:

- Server reboot → ❌ Data lost
- Power failure → ❌ Data lost
- Instance terminated → ❌ Data lost

With persistence enabled:

- Server reboot → ✅ Data restored
- Crash recovery → ✅ Possible
- Scheduled backups → ✅ Available

---

# Why Persistence Matters

Persistence helps protect:

- Cached application data (when needed)
- Queue jobs
- Session data (if retained)
- Application metadata
- Temporary business data

> **Important:** Redis is still not a replacement for a relational database like MySQL or PostgreSQL. Store permanent business records in your primary database.

---

# Redis Persistence Methods

Redis supports three persistence strategies:

| Method | Performance | Durability | Use Case |
|---------|-------------|------------|----------|
| RDB | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | Scheduled snapshots |
| AOF | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Maximum durability |
| Hybrid | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Recommended for production |

---

# RDB (Redis Database Snapshot)

RDB periodically saves the dataset to a binary snapshot file (`dump.rdb`).

## Advantages

- Fast startup
- Compact backup file
- Low disk usage
- Minimal runtime overhead

## Disadvantages

- Data written after the last snapshot may be lost if Redis crashes.

---

## Configure RDB

Open the configuration file.

```bash
sudo nano /etc/redis/redis.conf
```

Locate the `save` directives.

```ini
save 900 1
save 300 10
save 60 10000
```

Meaning:

| Rule | Description |
|------|-------------|
| save 900 1 | Save after 1 change in 900 seconds |
| save 300 10 | Save after 10 changes in 300 seconds |
| save 60 10000 | Save after 10,000 changes in 60 seconds |

---

## RDB File Location

Find the working directory:

```ini
dir /var/lib/redis
```

Default snapshot file:

```text
/var/lib/redis/dump.rdb
```

---

# AOF (Append Only File)

AOF logs every write operation.

Instead of periodic snapshots, Redis replays commands to rebuild the dataset.

## Advantages

- Better durability
- Lower risk of data loss
- Easier recovery after crashes

## Disadvantages

- Larger file size
- Slightly slower writes

---

## Enable AOF

Edit `redis.conf`.

```ini
appendonly yes
```

Default file name:

```ini
appendfilename "appendonly.aof"
```

Restart Redis.

```bash
sudo systemctl restart redis-server
```

---

## Configure AOF Sync Policy

Locate:

```ini
appendfsync everysec
```

Available options:

| Setting | Description |
|---------|-------------|
| always | Sync every write (maximum durability, slower) |
| everysec | Sync every second (recommended) |
| no | Let the OS decide (fastest, less durable) |

Recommended:

```ini
appendfsync everysec
```

---

# Hybrid Persistence

Hybrid persistence combines:

- RDB snapshots
- AOF logging

Benefits:

- Faster restarts than pure AOF
- Better durability than RDB alone

Modern Redis versions enable optimized AOF rewrite behavior by default.

Recommended for production.

---

# Restart Redis

After changing persistence settings:

```bash
sudo systemctl restart redis-server
```

Check status:

```bash
sudo systemctl status redis-server
```

---

# Verify Persistence

Open Redis CLI.

```bash
redis-cli
```

Run:

```bash
INFO persistence
```

Example output:

```text
loading:0
rdb_bgsave_in_progress:0
aof_enabled:1
```

---

# Check Persistence Files

RDB

```bash
ls -lh /var/lib/redis/dump.rdb
```

AOF

```bash
ls -lh /var/lib/redis/appendonly.aof
```

---

# Backup Redis Data

Create a backup directory.

```bash
sudo mkdir -p /backup/redis
```

Backup RDB.

```bash
sudo cp /var/lib/redis/dump.rdb /backup/redis/
```

Backup AOF.

```bash
sudo cp /var/lib/redis/appendonly.aof /backup/redis/
```

Compress backups.

```bash
sudo tar -czf redis-backup.tar.gz /backup/redis
```

---

# Restore Redis Data

Stop Redis.

```bash
sudo systemctl stop redis-server
```

Restore the persistence file.

```bash
sudo cp dump.rdb /var/lib/redis/
```

or

```bash
sudo cp appendonly.aof /var/lib/redis/
```

Ensure ownership is correct.

```bash
sudo chown redis:redis /var/lib/redis/dump.rdb
```

Start Redis.

```bash
sudo systemctl start redis-server
```

Verify data.

```bash
redis-cli INFO persistence
```

---

# Automatic Backups

Example cron job:

```bash
sudo crontab -e
```

Daily backup at 2:00 AM.

```cron
0 2 * * * cp /var/lib/redis/dump.rdb /backup/redis/dump-$(date +\%F).rdb
```

Regularly clean up old backups to prevent disk space issues.

---

# Production Recommendations

## Use RDB

Suitable for:

- Cache-only workloads
- Easy backup and restore
- Fast startup

---

## Use AOF

Suitable for:

- Queue systems
- Session storage
- Important temporary application data

---

## Use Hybrid Persistence

Recommended for most production deployments.

Benefits:

- Better durability
- Faster recovery
- Balanced performance

---

# 📊 Redis Monitoring Guide

> Monitoring is essential for maintaining a healthy Redis instance in production. This guide covers Redis performance monitoring, memory usage, client connections, slow queries, Prometheus integration, Grafana dashboards, and alerting best practices.

---

# Table of Contents

1. Why Monitor Redis?
2. Basic Health Check
3. Memory Monitoring
4. Connected Clients
5. Server Statistics
6. Keyspace Statistics
7. Slow Log Monitoring
8. Latency Monitoring
9. Real-Time Command Monitoring
10. Prometheus Integration
11. Grafana Dashboard
12. Alerting
13. Useful Commands
14. Production Best Practices
15. Production Checklist

---

# Why Monitor Redis?

Monitoring helps you detect:

- High memory usage
- Slow commands
- Connection issues
- Expired keys
- Evictions
- High CPU usage
- Replication problems
- Unexpected downtime

Without monitoring, Redis issues may go unnoticed until they affect your application.

---

# Basic Health Check

Verify Redis is running.

```bash
sudo systemctl status redis-server
```

Check service health.

```bash
redis-cli ping
```

Expected Output

```text
PONG
```

---

# Memory Monitoring

Display memory statistics.

```bash
redis-cli INFO memory
```

Important metrics:

| Metric | Description |
|---------|-------------|
| used_memory | Current memory usage |
| used_memory_peak | Highest memory usage |
| maxmemory | Configured memory limit |
| mem_fragmentation_ratio | Memory fragmentation |

---

# Configure Memory Limit

Edit Redis configuration.

```bash
sudo nano /etc/redis/redis.conf
```

Example:

```ini
maxmemory 512mb
```

Configure eviction policy.

```ini
maxmemory-policy allkeys-lru
```

Restart Redis.

```bash
sudo systemctl restart redis-server
```

---

# Connected Clients

Check connected clients.

```bash
redis-cli INFO clients
```

Example Output

```text
connected_clients:5
blocked_clients:0
```

List client details.

```bash
redis-cli CLIENT LIST
```

---

# Server Statistics

View general statistics.

```bash
redis-cli INFO stats
```

Important metrics:

| Metric | Description |
|---------|-------------|
| total_connections_received | Total connections |
| total_commands_processed | Commands executed |
| instantaneous_ops_per_sec | Commands per second |
| expired_keys | Keys expired |
| evicted_keys | Keys removed due to memory pressure |

---

# Keyspace Statistics

View database usage.

```bash
redis-cli INFO keyspace
```

Example:

```text
db0:keys=1523,expires=1200
```

This helps track:

- Total keys
- Expiring keys
- Database utilization

---

# Slow Log Monitoring

Redis records commands that exceed the configured execution time.

View slow commands.

```bash
redis-cli SLOWLOG GET
```

Check slow log length.

```bash
redis-cli SLOWLOG LEN
```

Reset slow log.

```bash
redis-cli SLOWLOG RESET
```

---

# Configure Slow Log

Edit configuration.

```bash
sudo nano /etc/redis/redis.conf
```

Example:

```ini
slowlog-log-slower-than 10000
```

Unit:

```
Microseconds
```

Example:

```
10000 = 10 milliseconds
```

---

# Latency Monitoring

Run latency doctor.

```bash
redis-cli --latency
```

Or:

```bash
redis-cli LATENCY DOCTOR
```

Useful for detecting:

- CPU bottlenecks
- Disk delays
- System load issues

---

# Real-Time Command Monitoring

Monitor all Redis commands.

```bash
redis-cli MONITOR
```

Example Output

```text
SET user:1
GET user:1
DEL session:10
```

> **Warning:** `MONITOR` is resource-intensive. Avoid running it continuously in production.

---

# Check Persistence Status

Verify persistence.

```bash
redis-cli INFO persistence
```

Important fields:

- rdb_last_save_time
- aof_enabled
- loading
- rdb_bgsave_in_progress

---

# Prometheus Integration

Install Redis Exporter.

```bash
docker run -d \
  --name redis-exporter \
  -p 9121:9121 \
  oliver006/redis_exporter
```

Or install directly on the server.

The exporter exposes Redis metrics in Prometheus format.

Example endpoint:

```
http://localhost:9121/metrics
```

---

# Prometheus Configuration

Add Redis Exporter as a scrape target.

```yaml
scrape_configs:
  - job_name: redis
    static_configs:
      - targets:
          - localhost:9121
```

Restart Prometheus after updating the configuration.

---

# Grafana Dashboard

Recommended panels:

- Redis Uptime
- Memory Usage
- Connected Clients
- Commands Per Second
- Key Count
- CPU Usage
- Network Traffic
- Evicted Keys
- Expired Keys
- Slow Commands
- Cache Hit Ratio

Grafana provides official community dashboards for Redis monitoring.

---

# Alerting

Recommended alerts:

| Alert | Threshold |
|--------|-----------|
| Redis Down | Immediate |
| Memory Usage | >80% |
| Connected Clients | Unusual increase |
| Evicted Keys | >0 |
| Slow Commands | High frequency |
| High CPU Usage | >85% |
| Replication Failure | Immediate |

Alert channels:

- Email
- Slack
- Microsoft Teams
- PagerDuty
- Opsgenie

---

# Useful Commands

General information.

```bash
redis-cli INFO
```

Memory.

```bash
redis-cli INFO memory
```

Clients.

```bash
redis-cli INFO clients
```

Statistics.

```bash
redis-cli INFO stats
```

Keyspace.

```bash
redis-cli INFO keyspace
```

Persistence.

```bash
redis-cli INFO persistence
```

Server.

```bash
redis-cli INFO server
```

Configuration.

```bash
redis-cli CONFIG GET *
```

Logs.

```bash
sudo journalctl -u redis-server
```

---

# Production Best Practices

- Monitor Redis 24/7.
- Set memory limits to prevent OOM issues.
- Configure an appropriate eviction policy.
- Monitor slow commands regularly.
- Avoid using `MONITOR` continuously in production.
- Integrate Redis Exporter with Prometheus.
- Visualize metrics using Grafana.
- Configure alerts for critical events.
- Review logs regularly.
- Test alert notifications periodically.


# 💾 Redis Backup & Restore Guide

> Backups are essential for protecting Redis data against accidental deletion, server failure, corruption, or disaster recovery events. This guide covers manual backups, automated backups, restore procedures, and production best practices.

---

# Table of Contents

1. Why Backup Redis?
2. Understanding Redis Persistence
3. Backup Strategies
4. Manual Backup
5. Automated Backup
6. Scheduled Backups with Cron
7. Backup Compression
8. Backup Verification
9. Restore Redis Data
10. Disaster Recovery
11. AWS Backup Strategy
12. Production Best Practices
13. Production Checklist

---

# Why Backup Redis?

Although Redis is commonly used for caching, many production systems also use it for:

- Queue jobs
- Session storage
- Rate limiting data
- Temporary business data
- Leaderboards
- Real-time analytics

Without backups:

- Server failure may cause data loss.
- Disk corruption can destroy persistence files.
- Human error (e.g., accidental deletion) can impact applications.
- Recovery time increases during incidents.

---

# Understanding Redis Persistence

Redis stores data using one or both of these persistence methods:

| Method | File |
|--------|------|
| RDB | `dump.rdb` |
| AOF | `appendonly.aof` |

Default directory:

```text
/var/lib/redis/
```

---

# Check Persistence Status

Verify persistence before creating backups.

```bash
redis-cli INFO persistence
```

Important fields:

```text
rdb_last_save_time
aof_enabled
loading
```

---

# Manual Backup

Create a backup directory.

```bash
sudo mkdir -p /backup/redis
```

Backup the RDB snapshot.

```bash
sudo cp /var/lib/redis/dump.rdb /backup/redis/
```

Backup the AOF file (if enabled).

```bash
sudo cp /var/lib/redis/appendonly.aof /backup/redis/
```

Verify the backup.

```bash
ls -lh /backup/redis
```

---

# Create Timestamped Backups

Use the current date in the filename.

```bash
sudo cp /var/lib/redis/dump.rdb \
/backup/redis/dump-$(date +%F-%H-%M).rdb
```

Example:

```text
dump-2026-07-15-02-00.rdb
```

---

# Compress Backup Files

Compress to save disk space.

```bash
gzip /backup/redis/dump-2026-07-15-02-00.rdb
```

Or archive multiple files.

```bash
tar -czf redis-backup.tar.gz /backup/redis
```

---

# Automated Backup with Cron

Open the root crontab.

```bash
sudo crontab -e
```

Create a daily backup at 2:00 AM.

```cron
0 2 * * * cp /var/lib/redis/dump.rdb /backup/redis/dump-$(date +\%F).rdb
```

Weekly compressed backup.

```cron
0 3 * * 0 tar -czf /backup/redis/redis-$(date +\%F).tar.gz /var/lib/redis
```

---

# Verify Backup Integrity

Ensure backup files exist.

```bash
ls -lh /backup/redis
```

Check archive integrity.

```bash
gzip -t backup.rdb.gz
```

Or verify tar archives.

```bash
tar -tf redis-backup.tar.gz
```

Regularly test backup restoration to ensure backups are usable.

---

# Restore Redis Data

## Step 1 — Stop Redis

```bash
sudo systemctl stop redis-server
```

---

## Step 2 — Restore the Persistence File

Restore the RDB file.

```bash
sudo cp dump.rdb /var/lib/redis/
```

Or restore the AOF file.

```bash
sudo cp appendonly.aof /var/lib/redis/
```

---

## Step 3 — Set File Ownership

```bash
sudo chown redis:redis /var/lib/redis/dump.rdb
```

If restoring AOF:

```bash
sudo chown redis:redis /var/lib/redis/appendonly.aof
```

---

## Step 4 — Start Redis

```bash
sudo systemctl start redis-server
```

Verify the service.

```bash
sudo systemctl status redis-server
```

---

## Step 5 — Verify Data

Check Redis status.

```bash
redis-cli ping
```

Expected Output

```text
PONG
```

Review persistence information.

```bash
redis-cli INFO persistence
```

---

# Disaster Recovery

A recommended disaster recovery workflow:

1. Stop Redis.
2. Restore the latest verified backup.
3. Set correct ownership and permissions.
4. Start Redis.
5. Validate application functionality.
6. Review Redis logs for errors.
7. Confirm data integrity.

Document and regularly test this procedure.

---

# AWS Backup Strategy

For AWS EC2 deployments:

```text
Redis
      │
      ▼
Persistence Files
      │
      ▼
Daily Backup
      │
      ▼
Compress
      │
      ▼
Amazon S3
      │
      ▼
Cross-Region Replication (Optional)
```

Recommendations:

- Store backups outside the EC2 instance.
- Use Amazon S3 lifecycle policies to transition old backups to lower-cost storage.
- Encrypt backups at rest and in transit.
- Periodically test restoring backups from S3.

---

# Recommended Retention Policy

| Backup Type | Retention |
|-------------|-----------|
| Daily | 7 Days |
| Weekly | 4 Weeks |
| Monthly | 12 Months |

Adjust the policy to match your business and compliance requirements.

---

# Production Best Practices

- Enable Redis persistence.
- Store backups on separate storage.
- Encrypt backup files.
- Schedule automatic backups.
- Verify backup integrity.
- Test restore procedures regularly.
- Monitor available disk space.
- Limit access to backup files.
- Include Redis in your disaster recovery plan.
- Document backup and restore procedures.


# 🛠️ Redis Troubleshooting Guide

> This guide covers the most common Redis issues encountered in production environments, along with practical troubleshooting steps and recommended solutions.

---

# Table of Contents

1. Troubleshooting Workflow
2. Check Redis Service
3. Check Redis Logs
4. Connection Refused
5. Authentication Failed
6. Redis Not Listening on Port 6379
7. High Memory Usage
8. Out of Memory (OOM)
9. Slow Performance
10. Persistence Problems
11. High CPU Usage
12. Too Many Connections
13. Permission Issues
14. Configuration Errors
15. Useful Diagnostic Commands
16. Production Best Practices
17. Production Checklist

---

# Troubleshooting Workflow

Before changing anything, follow this order:

1. Verify the service is running.
2. Review recent logs.
3. Check configuration.
4. Verify network connectivity.
5. Check memory and CPU usage.
6. Confirm authentication.
7. Test Redis using `redis-cli`.
8. Apply the fix.
9. Verify application functionality.
10. Document the incident.

---

# Check Redis Service

Check service status.

```bash
sudo systemctl status redis-server
```

If Redis is stopped:

```bash
sudo systemctl start redis-server
```

Restart Redis.

```bash
sudo systemctl restart redis-server
```

Enable on boot.

```bash
sudo systemctl enable redis-server
```

---

# Check Redis Logs

View recent logs.

```bash
sudo journalctl -u redis-server
```

Follow logs in real time.

```bash
sudo journalctl -fu redis-server
```

Look for:

- Startup failures
- Permission errors
- Memory issues
- Persistence failures
- Authentication failures

---

# Connection Refused

### Error

```text
Could not connect to Redis at 127.0.0.1:6379
Connection refused
```

### Possible Causes

- Redis service is stopped
- Wrong port
- Firewall blocking access
- Incorrect bind configuration

### Solution

Check service.

```bash
sudo systemctl status redis-server
```

Verify listening port.

```bash
sudo ss -tulpn | grep 6379
```

Check configuration.

```bash
sudo nano /etc/redis/redis.conf
```

Verify:

```ini
bind 127.0.0.1 ::1
```

Restart Redis.

```bash
sudo systemctl restart redis-server
```

---

# Authentication Failed

### Error

```text
NOAUTH Authentication required.
```

### Solution

Authenticate.

```bash
redis-cli
```

```bash
AUTH YourStrongRedisPassword123!
```

Verify configuration.

```bash
sudo nano /etc/redis/redis.conf
```

```ini
requirepass YourStrongRedisPassword123!
```

Restart Redis.

```bash
sudo systemctl restart redis-server
```

---

# Redis Not Listening on Port 6379

Check listening ports.

```bash
sudo ss -tulpn | grep 6379
```

If nothing appears:

Check configuration.

```ini
port 6379
```

Restart Redis.

```bash
sudo systemctl restart redis-server
```

---

# High Memory Usage

Check memory.

```bash
redis-cli INFO memory
```

Look at:

- used_memory
- maxmemory
- mem_fragmentation_ratio

Set a memory limit.

```ini
maxmemory 512mb
```

Choose an eviction policy.

```ini
maxmemory-policy allkeys-lru
```

Restart Redis.

```bash
sudo systemctl restart redis-server
```

---

# Out of Memory (OOM)

### Error

```text
OOM command not allowed
```

### Cause

Redis reached the configured memory limit.

### Solution

Check memory.

```bash
redis-cli INFO memory
```

Increase memory if appropriate.

```ini
maxmemory 1gb
```

Or free unused keys.

---

# Slow Performance

Check slow log.

```bash
redis-cli SLOWLOG GET
```

Check latency.

```bash
redis-cli --latency
```

Review command statistics.

```bash
redis-cli INFO commandstats
```

Common causes:

- Large keys
- Slow disks
- Insufficient memory
- High CPU usage

---

# Persistence Problems

Check persistence.

```bash
redis-cli INFO persistence
```

Verify RDB.

```bash
ls -lh /var/lib/redis/dump.rdb
```

Verify AOF.

```bash
ls -lh /var/lib/redis/appendonly.aof
```

Review logs.

```bash
sudo journalctl -u redis-server
```

---

# High CPU Usage

Check Redis process.

```bash
top
```

Or

```bash
htop
```

Identify expensive commands.

```bash
redis-cli INFO commandstats
```

Monitor live commands (short-term only).

```bash
redis-cli MONITOR
```

> **Warning:** Avoid running `MONITOR` continuously in production because it can significantly impact performance.

---

# Too Many Connections

Check clients.

```bash
redis-cli INFO clients
```

List clients.

```bash
redis-cli CLIENT LIST
```

Check limit.

```bash
redis-cli CONFIG GET maxclients
```

Increase if necessary.

```ini
maxclients 10000
```

Restart Redis.

---

# Permission Issues

Check ownership.

```bash
ls -ld /var/lib/redis
```

Correct ownership.

```bash
sudo chown -R redis:redis /var/lib/redis
```

Check permissions.

```bash
sudo chmod 750 /var/lib/redis
```

Restart Redis.

---

# Configuration Errors

Test configuration after making changes.

```bash
sudo systemctl restart redis-server
```

If Redis fails to start:

```bash
sudo journalctl -xe
```

Review the configuration file.

```bash
sudo nano /etc/redis/redis.conf
```

Restore from backup if needed.

---

# Useful Diagnostic Commands

Redis version.

```bash
redis-server --version
```

Health check.

```bash
redis-cli ping
```

General information.

```bash
redis-cli INFO
```

Memory.

```bash
redis-cli INFO memory
```

Clients.

```bash
redis-cli INFO clients
```

Statistics.

```bash
redis-cli INFO stats
```

Persistence.

```bash
redis-cli INFO persistence
```

Logs.

```bash
sudo journalctl -u redis-server
```

Listening port.

```bash
sudo ss -tulpn | grep 6379
```

Process.

```bash
ps aux | grep redis
```

---

# Production Best Practices

- Monitor Redis continuously.
- Enable persistence where appropriate.
- Keep Redis updated.
- Restrict access using Security Groups and firewalls.
- Use authentication with a strong password.
- Configure memory limits and eviction policies.
- Avoid using `KEYS *` in production; prefer `SCAN`.
- Avoid running `MONITOR` for long periods.
- Test backups and restore procedures regularly.
- Document every production incident and resolution.


