---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Docker



## Docker - How to

### Images

#### Build image

```bash
docker build <dir-with-Dockerfile>
```

#### List images

`docker images` is an alias of `docker image ls`

```bash
docker images
```

#### Delete image

```bash
docker rmi IMAGE
docker rmi -f IMAGE  # To force even though there are containers using the image
```

### Containers

#### List containers

`docker ps` is an alias to the command `docker container ls`

```bash
docker ps ls
docker ps ls -a  # Also list non-running containers
```

#### Run container directly from an image

```bash
docker run --rm -it ubuntu:latest bash
```

#### Delete container&#x20;

```bash
docker rm CONTAINER
```

#### Execute command in a docker container

```bash
docker exec [OPTIONS] <container> <command> [ARGS]
```

#### Open a shell in a container

```bash
docker exec -it <container> bash
```

#### Run a container

TODO

#### Open bash in container

```bash
docker exec -it <container_name> bash

# As root
docker exec -it -u 0 <container_name>
```

## Volumes

```
docker volume ls
docker volume rm <name>
```

## Docker compose - How to

{% hint style="warning" %}
This applies to docker compose version 1
{% endhint %}

### Build container

```bash
docker compose build <service name>
```

### Start all containers

```bash
docker-compose up
docker-compose up -d  # in background
```

## TODO

```bash
docker system prune
```
