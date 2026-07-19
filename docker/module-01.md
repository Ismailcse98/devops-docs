## Module 1: Docker Fundamentals

By the end of this module, you should be able to answer:

    - What is Docker?
    - Why do developers use Docker?
    - What problem does Docker solve?
    - What is the difference between Docker and a Virtual Machine?
    - What are Images, Containers, Volumes, and Networks?
    - How does Docker work internally?
    - What are the most common Docker commands?

## What is Docker?

Imagine you built a Laravel project on your laptop.
It works perfectly.
You send it to another developer.
They try to run it and get errors like:

    - PHP version is different.
    - Composer version is different.
    - MySQL version is different.
    - Redis isn't installed.
    - Required PHP extensions are missing.

This is the classic "It works on my machine" problem.

Docker solves this by packaging your application and everything it needs into a container.

A Docker container includes:

    - Operating system libraries
    - PHP
    - Composer
    - Required PHP extensions
    - Application code
    - Configuration files

If Docker works on your computer, the same container will work on another developer's machine, a testing server, or a production server.

## Why Docker?

| Developer A | Developer B |
|-------------|-------------|
| Ubuntu | Windows |
| PHP 8.2 | PHP 8.1 |
| MySQL 8 | MySQL 5.7 |

Application breaks

With Docker:

    Docker Image -> Developer A -> Developer B -> Production Server -> Everything works the same

Docker provides a consistent environment everywhere.

## What Problems Does Docker Solve?
Docker helps solve many common issues:

    - Different PHP versions
    - Missing PHP extensions
    - Different MySQL versions
    - Redis not installed
    - Different operating systems
    - Manual environment setup
    - Deployment inconsistencies

Instead of asking teammates to install everything manually, you share your Docker configuration.

## What is a Container?

A container is a running instance of an application inside an isolated environment.

Think of it like a lunch box.

The lunch box contains everything needed for your meal.

Similarly, a Docker container contains everything needed to run your application.

Example:

Container

    ├── PHP 8.2
    ├── Composer
    ├── Laravel
    ├── Extensions
    └── Configuration
Each container is isolated from the others.

## What is an Image?
An image is a blueprint or template used to create containers.

> Relationship: Image -> Container -> Running Application

One image can create many containers.
Example:

    PHP Image
        ├── Container 1
        ├── Container 2
        ├── Container 3

## Image vs Container

| Image | Container |
|-------------|-------------|
| Blueprint | Running application |
| Read-only | Writable while running |
| Used to create containers | Created from an image |
| Doesn't execute | Executes processes |

## What is Docker Hub?
Docker Hub is an online registry where Docker images are stored and shared.

Examples of official images:

    - PHP
    - MySQL
    - Redis
    - Nginx
    - Ubuntu
    - Node.js

Later, we'll pull these images instead of installing everything manually.

## Docker Engine
Docker Engine is the software that manages Docker on your machine.

It is responsible for:

    - Building images
    - Running containers
    - Managing networks
    - Managing volumes
    - Pulling images
    - Removing containers

You interact with Docker Engine using commands like:
```base
docker ps
docker run
docker build
```

## Docker Client and Docker Daemon
When you type:
```bash
docker run nginx
```

The flow is:
```text
You
   ↓
Docker CLI
   ↓
Docker Daemon
   ↓
Docker Engine
   ↓
Container Starts
```
- Docker CLI: The command-line tool you use.
- Docker Daemon: The background service that does the actual work.
- Docker Engine: The platform that manages everything.

## Container Lifecycle

A container goes through several states:
```text
Image
   ↓
Create
   ↓
Start
   ↓
Running
   ↓
Stopped
   ↓
Removed
```
We'll learn commands for each state in later chapters.

## What is a Dockerfile?
A Dockerfile is a text file containing instructions to build a Docker image.

Example:
```bash
FROM php:8.2-fpm
WORKDIR /var/www
COPY . .
CMD ["php", "-v"]
```

## What is Docker Compose?
Most Laravel projects need multiple services:
- PHP
- Nginx
- MySQL
- Redis
- Mailpit

Starting each one manually would be tedious.
Docker Compose lets you define and run all services together using a single file:
```text
docker-compose.yml
```

With one command, everything starts:
```text
docker compose up -d
```

## What is a Volume?
Containers are temporary.

If a MySQL container is removed, its data would normally be lost.

A volume stores data outside the container so it persists.

Example:
```text
Container
      ↓
Volume
      ↓
Database Files
```

We'll use volumes for:
- MySQL data
- Redis data (optional)
- Application code

## What is a Network?
Containers communicate through Docker networks.

Instead of using localhost, containers use service names.

Example:
```text
Laravel
  ↓
mysql
  ↓
Redis
  ↓
Nginx
```

## Bind Mount vs Volume
There are two common ways to share data:

### Bind Mount

Uses a folder from your computer.

Example:
```text
Your Laptop
    ↓
Laravel Project
    ↓
Container
```

Changes on your computer appear immediately in the container.

Useful for development.

### Volume

Managed by Docker.

Best for persistent data like databases.