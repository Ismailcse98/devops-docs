# Docker Command List

## Module 1 — Docker Basics

Shows the installed Docker version. Use this first when setting up a new machine or debugging Docker installation.
```bash
docker --version
```
Shows Docker Engine information, storage driver, containers, images, resources, etc. Useful for general troubleshooting.
```bash
docker info
```
Shows both Docker Client and Docker Server/Engine versions. Useful when client/server compatibility may be causing problems.
```bash
docker version
```

## Module 2 — Docker Images
Shows all locally available Docker images.
```bash
docker images
```
Shows all locally available Docker images.
```bash
docker images || docker image ls
```
Searches Docker Hub for images.
```bash
docker search nginx
```
Downloads the latest Nginx image from Docker Hub.
```bash
docker pull nginx
```
Downloads a specific PHP-FPM version
```bash
docker pull php:8.2-fpm
```
Removes an image when no container is using it.
```bash
docker rmi nginx
```
Removes an image when no container is using it.
```bash
docker image rm nginx
```
Force-removes the image. Use carefully because dependent containers may be affected.
```bash
docker rmi -f nginx
```
Shows image metadata, architecture, layers, environment variables, etc.
```bash
docker image inspect nginx
```
Shows the image's build layers. Very useful when debugging large Docker images.
```bash
docker history nginx
```
Removes dangling/unused images.
```bash
docker image prune
```
Removes all images not currently used by containers.
```bash
docker image prune -a
```

## Module 3 — Running Containers

Start a container: Creates and starts an Nginx container in the foreground.
```bash
docker run nginx
```
Run in background: Creates and starts an Nginx container in the background.
```bash
docker run -d nginx
```
Give container a name: Naming containers makes management easier.
```bash
docker run -d --name my-nginx nginx
```
Port mapping: This is extremely common when running Laravel/Nginx (http://localhost:8080)
```bash
docker run -d --name my-nginx -p 8080:80 nginx
```
Environment variable: -e passes environment variables into the container.
```bash
docker run -d --name mysql -e MYSQL_ROOT_PASSWORD=secret mysql:8
```
Run interactive container: Useful when learning Linux inside containers or debugging an image.
```bash
docker run -it ubuntu bash
```
Run and automatically remove: Container is automatically deleted when it stops. Excellent for temporary testing.
```bash
docker run --rm nginx
```
## Module 4 — Container Management
List running containers: Most frequently used Docker command.
```bash
docker ps
```
List all containers: Shows running + stopped containers.
```bash
docker ps -a
```
Container names and IDs: Useful when you have many containers.
```bash
docker ps --format "table {{.ID}}\t{{.Names}}\t{{.Status}}"
```
Start: Starts an existing stopped container.
```bash
docker start my-nginx
```
Stop: Gracefully stops the container.
```bash
docker stop my-nginx
```
Restart: Restarts an existing container.
```bash
docker restart my-nginx
```
Kill: Immediately terminates the container. Use stop normally; use kill when the container refuses to stop.
```bash
docker kill my-nginx
```
Pause: Freezes processes inside the container.
```bash
docker pause my-nginx
```
Unpause: Resumes paused processes.
```bash
docker unpause my-nginx
```

## Module 5 — Delete Containers
Remove stopped container: Deletes the container.
```bash
docker rm my-nginx
```
Force remove running container: Stops and removes it.
```bash
docker rm -f my-nginx
```
Remove all stopped containers: Useful for cleaning development machines.
```bash
docker container prune
```
## Module 6 — Container Debugging

# It will be constantly updated.




