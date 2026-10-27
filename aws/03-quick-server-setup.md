# Quick Server Setup

## Create .sh file
```bash
nano setup.sh
```

## Copy & Past this script
```bash

#!/bin/bash
set -e

# Must run as root
if [ "$EUID" -ne 0 ]; then
    echo "Please run: sudo bash setup.sh"
    exit 1
fi

export DEBIAN_FRONTEND=noninteractive

echo "===== Updating packages ====="
apt-get update

echo "===== Installing basic tools ====="
apt-get install -y \
    curl git unzip ca-certificates \
    nginx certbot mysql-client redis-tools

echo "===== Installing PHP 8.3 if missing ====="
if ! command -v php >/dev/null 2>&1; then
    apt-get install -y \
        php8.3-cli php8.3-mysql php8.3-redis \
        php8.3-curl php8.3-mbstring php8.3-xml \
        php8.3-zip php8.3-bcmath
fi

echo "===== Installing Docker if missing ====="
if ! command -v docker >/dev/null 2>&1; then
    apt-get install -y docker.io
fi

echo "===== Installing Docker Compose if missing ====="
if ! docker compose version >/dev/null 2>&1; then
    apt-get install -y docker-compose-v2
fi

echo "===== Starting Docker ====="
systemctl enable --now docker

echo "===== Adding ubuntu user to Docker group ====="
if id ubuntu >/dev/null 2>&1; then
    usermod -aG docker ubuntu
    echo "ubuntu user added to docker group"
fi

echo "===== Starting Nginx test container ====="
if docker ps -a --format '{{.Names}}' | grep -qx nginx-test; then
    docker start nginx-test || true
else
    # Stop host Nginx to free port 80 for Docker Nginx
    systemctl disable --now nginx || true

    docker run -d \
        --name nginx-test \
        --restart unless-stopped \
        -p 80:80 \
        nginx:alpine
fi

echo ""
echo "===== Installation Complete ====="
echo "PHP:"
php -v

echo ""
echo "Docker:"
docker --version

echo ""
echo "Docker Compose:"
docker compose version

echo ""
echo "Certbot:"
certbot --version

echo ""
echo "Running containers:"
docker ps

echo ""
echo "Open in browser:"
echo "http://YOUR_EC2_PUBLIC_IP/"
echo ""
echo "IMPORTANT: Reconnect SSH to apply Docker group permissions."
echo "Docker group members have root-level privileges."

```

## Set permission in script file
```bash
chmod +x setup.sh
```

## Execute script file
```bash
sudo ./setup.sh
```

## Open your browser and See Nginx default page
```base
http://YOUR_EC2_PUBLIC_IP
```