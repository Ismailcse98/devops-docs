# Docker Commands

## Docker Essential Commands

```text
| Command                          | Description                                                  |
| -------------------------------- | ------------------------------------------------------------ |
|   docker version                 | Displays Docker client and server versions.                  |
|   docker info                    | Displays Docker environment information.                     |
|   docker images                  | Lists local Docker images.                                   |
|   docker pull nginx              | Downloads an image from a container registry.                |
|   docker build -t app .          | Builds a Docker image from a Dockerfile.                     |
|   docker run nginx               | Creates and starts a container from an image.                |
|   docker ps                      | Lists running containers.                                    |
|   docker ps -a                   | Lists running and stopped containers.                        |
|   docker stop container          | Gracefully stops a container.                                |
|   docker start container         | Starts a stopped container.                                  |
|   docker restart container       | Restarts a container.                                        |
|   docker rm container            | Removes a container.                                         |
|   docker rmi image               | Removes a Docker image.                                      |
|   docker exec -it container bash | Opens an interactive shell inside a running container.       |
|   docker logs container          | Displays container logs.                                     |
|   docker logs -f container       | Continuously follows container logs.                         |
|   docker inspect container       | Displays detailed container configuration.                   |
|   docker stats                   | Displays real-time container CPU, memory, and network usage. |
|   docker network ls              | Lists Docker networks.                                       |
|   docker volume ls               | Lists Docker volumes.                                        |
|   docker system df               | Displays Docker disk usage.                                  |
|   docker system prune            | Removes unused Docker resources.                             |

```

## Docker Compose

```text
| Command                        | Description                                              |
| ------------------------------ | -------------------------------------------------------- |
|   docker compose up            | Creates and starts services defined in the Compose file. |
|   docker compose up -d         | Starts services in detached/background mode.             |
|   docker compose down          | Stops and removes Compose containers and networks.       |
|   docker compose ps            | Displays Compose service status.                         |
|   docker compose logs          | Displays service logs.                                   |
|   docker compose logs -f       | Continuously follows service logs.                       |
|   docker compose build         | Builds images defined by the Compose configuration.      |
|   docker compose pull          | Pulls required images.                                   |
|   docker compose restart       | Restarts Compose services.                               |
|   docker compose exec app bash | Opens a shell inside the `app` service container.        |

```
