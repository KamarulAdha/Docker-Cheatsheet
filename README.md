# Docker-Cheatsheet
Commands for Docker

# Comprehensive Docker Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Dockerfile](#dockerfile)
3. [Docker Commands](#docker-commands)
4. [Docker Compose](#docker-compose)
5. [Best Practices](#best-practices)

## Introduction

Docker is a platform for developing, shipping, and running applications in containers. Containers are lightweight, portable, and consistent environments that package an application and its dependencies.

## Dockerfile

A Dockerfile is a text file that contains instructions for building a Docker image.

```dockerfile
# Dockerfile example
FROM ubuntu:20.04
WORKDIR /app
COPY . /app
RUN apt-get update && apt-get install -y python3
CMD ["python3", "app.py"]
```

### Common Dockerfile Instructions

- `FROM`: Specifies the base image
- `WORKDIR`: Sets the working directory for subsequent instructions
- `COPY`: Copies files from host to the container
- `ADD`: Similar to COPY, but can also handle URLs and extract compressed files
- `RUN`: Executes commands in the container during build
- `ENV`: Sets environment variables
- `EXPOSE`: Informs Docker that the container listens on specified network ports
- `CMD`: Specifies the command to run when the container starts
- `ENTRYPOINT`: Configures the container to run as an executable

## Docker Commands

Note: Depending on your Docker installation and system configuration, you may need to use `sudo` before each Docker command. We've included `sudo` in the examples below, but you can omit it if your user has the necessary permissions.

### Building Images

```bash
# Build an image from a Dockerfile in the current directory
sudo docker build -t myimage:tag .

# Build an image from a Dockerfile in a specific directory
sudo docker build -t myimage:tag /path/to/dockerfile/directory
```

### Running Containers

```bash
# Run a container from an image
sudo docker run myimage:tag

# Run a container in detached mode (background)
sudo docker run -d myimage:tag

# Run a container with port mapping
sudo docker run -p 8080:80 myimage:tag

# Run a container with volume mounting
sudo docker run -v /host/path:/container/path myimage:tag

# Run a container with environment variables
sudo docker run -e VAR_NAME=value myimage:tag

# Run a container with a specific name
sudo docker run --name mycontainer myimage:tag

# Run a container and remove it when it exits
sudo docker run --rm myimage:tag
```

### Managing Containers

```bash
# List running containers
sudo docker ps

# List all containers (including stopped ones)
sudo docker ps -a

# Stop a running container
sudo docker stop container_id_or_name

# Start a stopped container
sudo docker start container_id_or_name

# Restart a container
sudo docker restart container_id_or_name

# Remove a container
sudo docker rm container_id_or_name

# Remove all stopped containers
sudo docker container prune
```

### Managing Images

```bash
# List images
sudo docker images

# Remove an image
sudo docker rmi image_id_or_name

# Remove all unused images
sudo docker image prune
```

### Logs and Debugging

```bash
# View container logs
sudo docker logs container_id_or_name

# Follow container logs (stream in real-time)
sudo docker logs -f container_id_or_name

# Execute a command in a running container
sudo docker exec -it container_id_or_name command
```

## Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications.

```yaml
# docker-compose.yml example
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"
  redis:
    image: "redis:alpine"
```

```bash
# Start services defined in docker-compose.yml
sudo docker-compose up

# Start services in detached mode
sudo docker-compose up -d

# Stop and remove containers, networks, and volumes
sudo docker-compose down

# View logs of all services
sudo docker-compose logs

# Execute a command in a service container
sudo docker-compose exec service_name command
```

## Best Practices

1. Use official base images when possible
2. Minimize the number of layers in your Dockerfile
3. Use multi-stage builds for smaller final images
4. Don't run containers as root
5. Use .dockerignore to exclude unnecessary files
6. Cache dependencies separately from application code
7. Use environment variables for configuration
8. Tag your images properly
9. Use Docker Compose for multi-container applications
10. Regularly update your images and dependencies

## Additional Tips

### .dockerignore

Create a `.dockerignore` file to exclude files and directories from the build context:

```
# .dockerignore example
node_modules
npm-debug.log
Dockerfile
.dockerignore
.git
.gitignore
```

### Docker Volumes

```bash
# Create a volume
sudo docker volume create myvolume

# Run a container with a volume
sudo docker run -v myvolume:/path/in/container myimage:tag

# List volumes
sudo docker volume ls

# Inspect a volume
sudo docker volume inspect myvolume

# Remove a volume
sudo docker volume rm myvolume
```

### Docker System Commands

```bash
# Display Docker disk usage
sudo docker system df

# Remove unused data
sudo docker system prune

# Remove all unused images, not just dangling ones
sudo docker system prune -a
```

This guide covers the essentials of Docker, including Dockerfile instructions, basic commands, Docker Compose usage, and best practices. Use it as a quick reference when working with Docker in your projects. Remember to adjust the use of `sudo` based on your system's configuration and permissions.