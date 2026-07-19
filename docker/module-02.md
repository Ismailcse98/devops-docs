# Module 2: Install Docker (Ubuntu)

By the end of this module, you will learn:

- Install Docker Engine from the official repository.
- Install Docker Compose.
- Understand what gets installed.
- Verify that Docker is working correctly.
- Run your first Docker container.
- Learn the basic Docker commands you'll use every day.

## Check Your Operating System

Before installing Docker, check your Ubuntu version.

```bash
lsb_release -a
```

OR

```bash
cat /etc/os-release
```

Example output:

```text
Distributor ID: Ubuntu
Description: Ubuntu 24.04 LTS
Release: 24.04
Codename: noble
```

## Remove Old Docker Versions

If Docker was previously installed, remove old packages.

```bash
sudo apt remove docker docker-engine docker.io containerd runc
```

Clean unused packages:

```bash
sudo apt autoremove -y
```

## Update Ubuntu

Always update package information before installing software.

```bash
sudo apt update
```

Upgrade installed packages:

```bash
sudo apt upgrade -y
```

## Install Required Packages

Install packages needed to add Docker's official repository.

```bash
sudo apt install -y ca-certificates curl gnupg lsb-release
```

What are these packages?

| Package         | Purpose                           |
| --------------- | --------------------------------- |
| ca-certificates | Verifies secure HTTPS connections |
| curl            | Downloads files from the internet |
| gnupg           | Verifies Docker's signing key     |
| lsb-release     | Detects Ubuntu version            |

## Add Docker GPG Key

Create the key directory:

```bash
sudo install -m 0755 -d /etc/apt/keyrings
```

Download Docker's official GPG key:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

Give the correct permission:

```bash
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

Why is the GPG key important?
It verifies that Docker packages come from Docker and haven't been tampered with.

## Add Docker Repository

```bash
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## Update Package Index Again

Ubuntu now knows about Docker's repository. Update package information:

```bash
sudo apt update
```

## Install Docker

Install Docker Engine and related tools.

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### What Was Installed?

Let's understand each package.

| Package               | Purpose                |
| --------------------- | ---------------------- |
| docker-ce             | Docker Engine          |
| docker-ce-cli         | Docker command line    |
| containerd.io         | Container runtime      |
| docker-buildx-plugin  | Advanced image builder |
| docker-compose-plugin | docker compose command |

## Verify Docker Installation

Check Docker version.

```bash
docker --version
```

Check Compose version.

```bash
docker compose version
```

## Check Docker Service

Check Docker status.

```bash
sudo systemctl status docker
```

If Docker isn't running:

```bash
sudo systemctl start docker
```

Enable Docker to start on boot:

```bash
sudo systemctl enable docker
```

## Run Your First Container

Let's run the official test container.

```bash
sudo docker run hello-world
```

Expected output:

```text
Hello from Docker!
```

## Avoid Using sudo (Recommended)

By default, Docker requires sudo.

Add your user to the Docker group.

```bash
sudo usermod -aG docker $USER
```

Apply the new group:
```base
newgrp docker
```

Now test:
```bash
docker run hello-world
```
No **sudo** should be required.

## Understanding the First Run
```bash
docker run hello-world
```

Docker performed these steps:
```text
1. Check if image exists locally
    ↓
2. Not found
    ↓
3. Download image from Docker Hub
    ↓
4. Create container
    ↓
5. Start container
    ↓
6. Display message
    ↓
7. Container exits
```

## Your First Docker Commands
Show Docker version
```bash
docker --version
```
Show Docker information
```bash
docker info
```
List downloaded images
```bash
docker images
```

List running containers
```bash
docker ps
```

List all containers
```bash
docker ps -a
```

Remove a container

Find its container ID:
```bash
docker ps -a
```

Then:
```bash
docker rm CONTAINER_ID
```

Remove an image
```bash
docker rmi hello-world
```
Or use the image ID:

```bash
docker rmi IMAGE_ID
```

## Pull an Image Without Running It
Download an image only.
```bash
docker pull nginx
```
Now check:
```bash
docker images
```

## Run an Nginx Container
```bash
docker run nginx
```
## Run a Container in Background
```bash
docker run -d nginx
```
-d means detached mode.

Now check:
```bash
docker ps
```
You'll see the Nginx container running.

## Stop a Running Container
First list running containers:
```bash
docker ps
```

Stop it:
```bash
docker stop CONTAINER_ID
```

Or by name:
```bash
docker stop CONTAINER_NAME
```

## Remove the Stopped Container
```bash
docker rm CONTAINER_ID
```
force remove:
```bash
docker rm -f container
```
