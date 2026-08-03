# Docker Images & Dockerfile Fundamentals

## What is a Docker Image?
```text
A Docker Image is a read-only template used to create containers. One image can create many containers.
```

## Where Do Images Come From?
There are two main sources:

1. Docker Hub
```bash
docker pull nginx
```

2. Build Your Own
```bash
docker build -t my-nginx .
```

## What is a Dockerfile?
A Dockerfile is a text file containing instructions for building an image.

Example:
```bash
FROM ubuntu

RUN apt update

CMD ["bash"]
```

## Create First Docker Project
Create a practice folder.
```text
docker-learning/
└── first-image/
```

Commands:
```bash
mkdir -p docker-learning/first-image
cd docker-learning/first-image
```

Create a Dockerfile.
```text
touch Dockerfile
```

## First Dockerfile
Open the Dockerfile and write:
```bash
FROM ubuntu

CMD ["echo", "Hello Docker!"]
```
## Build First Image
```bash
docker build -t hello-image .
```

## Build Context
Suppose your project is:
```text
first-image/

├── Dockerfile

├── app.php

└── index.html
```

When you run:
```text
docker build .
```
Docker sends everything in the current directory to the Docker Engine. This is called the Build Context.

## View the Image
```bash
docker images
```

## Run This Image
```bash
docker run hello-image
```
Output:
```text
Hello Docker!
```

## Understanding Image Layers
Every Dockerfile instruction creates a new layer.

Example:
```bash
FROM ubuntu

RUN apt update

RUN apt install -y curl

RUN apt install -y git
```

Layers:
```text
Layer 1
Ubuntu

↓

Layer 2
apt update

↓

Layer 3
Install curl

↓

Layer 4
Install git
```

## Why Layers Matter
Suppose you change only the last line:

```bash
RUN apt install -y vim
```

Docker does not rebuild everything.

It reuses previous layers and rebuilds only the changed layer and those after it.

This makes builds much faster.

## Docker Build Cache
Build the image again:
```bash
docker build -t hello-image .
```

You'll notice it's much faster.

Docker reused the cached layers.

This is called the build cache.

## Force a Rebuild
Ignore the cache:

```bash
docker build --no-cache -t hello-image .
```
Docker rebuilds every layer from scratch.

## Dockerfile Instructions
```text
| Instruction | Purpose                                   |
| ----------- | ----------------------------------------- |
| FROM        | Base image                                |
| RUN         | Execute commands during build             |
| CMD         | Default command when the container starts |
| COPY        | Copy files into the image                 |
| ADD         | Copy files (with extra features)          |
| WORKDIR     | Set the working directory                 |
| ENV         | Define environment variables              |
| EXPOSE      | Document the listening port               |
| ENTRYPOINT  | Main executable                           |
| USER        | Run as a specific user                    |

```
