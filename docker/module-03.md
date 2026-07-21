# Docker CLI Deep Dive

## Docker Command Structure

Most Docker commands follow this pattern:
```bash
docker <object> <command> [options]
```

Examples:
```bash
docker image ls
docker container ls
docker volume ls
docker network ls
```
Docker also provides shorter aliases:
```bash
docker images      # Same as: docker image ls
docker ps          # Same as: docker container ls
```

## Pull an Image
Download the latest Ubuntu image:
```bash
docker pull ubuntu
```
List downloaded images:
```bash
docker images
```

Example output:
```text
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
ubuntu        latest    xxxxxxxxxxxx   2 weeks ago   79MB
```

## Run a Container
Run Ubuntu:
```bash
docker run ubuntu
```
It exits immediately. Because Ubuntu doesn't have a long-running process by default. The container stops as soon as its main process finishes.

## Run an Interactive Container
Start Ubuntu with an interactive terminal:
```bash
docker run -it ubuntu bash
```
```text
Options:

-i = Interactive mode (keep STDIN open)
-t = Allocate a terminal
```

## Give a Container a Name
```bash
docker run -it --name ubuntu-test ubuntu bash
```
## List Containers
Running containers:
```bash
docker ps
```
All containers:
```bash
docker ps -a
```

## Start a Stopped Container
Start by ID:
```bash
docker start CONTAINER_ID
```

Or Start by name:
```bash
docker start ubuntu-test
```

## Stop a Running Container
```bash
docker stop ubuntu-test
```

## Restart a Container
```bash
docker restart ubuntu-test
```

## Remove a Container
Remove a stopped container:
```bash
docker rm ubuntu-test
```
Force remove a running container:
```bash
docker rm -f ubuntu-test
```

## Execute Commands Inside a Running Container
Run Nginx:
```bash
docker run -d --name nginx-test nginx
```

Enter the container:
```bash
docker exec -it nginx-test bash
```

Some images (like Alpine) don't include bash. Use:
```bash
docker exec -it CONTAINER_NAME sh
```

Check files:
```bash
ls
```

Exit:
```bash
exit
```

## View Container Logs
Display logs:
```bash
docker logs nginx-test
```

Follow logs in real time:
```bash
docker logs -f nginx-test
```

Last 20 lines:
```bash
docker logs --tail 20 nginx-test
```

## Inspect a Container
Detailed information:
```bash
docker inspect nginx-test
```

## View Resource Usage
Monitor running containers:
```bash
docker stats
```

## Copy Files Between Host and Container
Copy from your computer to the container:
```bash
docker cp test.txt nginx-test:/tmp/
```

Copy from the container to your computer:
```bash
docker cp nginx-test:/etc/nginx/nginx.conf .
```

## Remove Unused Resources
Remove stopped containers:
```bash
docker container prune
```

Remove unused images:
```bash
docker image prune
```

Remove unused volumes:
```bash
docker volume prune
```

Remove unused networks:
```bash
docker network prune
```

Remove everything unused:
```bash
docker system prune
```

Or include unused images:
```bash
docker system prune -a
```

## View Docker Events
Watch Docker activity:
```bash
docker events
```

## View Running Processes Inside a Container
```bash
docker top nginx-test
```

## View Port Mappings
```bash
docker port nginx-test
```
If no ports were published, nothing will be shown.


Later we'll use:
```bash
docker run -d -p 8080:80 nginx
```

This maps:
```text
Host:      8080
Container: 80
```

You can then visit:
```text
http://localhost:8080
```

# Common Docker CLI Commands

| Command         | Purpose                           |
| --------------- | --------------------------------- |
| docker images | List images |
| docker ps | Running containers |
| docker ps -a | All containers |
| docker run | Create and run a container |
| docker start | Start a stopped container |
| docker stop | Stop a container |
| docker restart | Restart a container |
| docker rm | Remove a container |
| docker rmi | Remove an image |
| docker exec | Run commands inside a container |
| docker logs | View logs |
| docker inspect | Detailed information |
| docker stats | Resource usage |
| docker top | Running processes |
| docker cp | Copy files |
| docker events | Live Docker events |
| docker system prune | Clean unused resources |



