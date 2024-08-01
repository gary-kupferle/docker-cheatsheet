# Docker Cheatsheet
Frequently used commands in the world according to Kup

#### Hello, Docker
```
# Copy (pull) a new image to Docker host
docker pull ubuntu:latest

# Check that the image is there
docker images

# Start a container (from the above image)
# -it makes it interactive and attach your shell to the container's terminal
# 'bash' at end tells Docker to start a bash shell
docker run --name test -it ubuntu:latest bash

# Exit the container, but do not terminate it
Ctrl-PQ

# Check that the container started above is still running after 'Ctrl-PQ'
docker ps

# Attach your shell to the above container (named 'test')
docker attach test

# Stop the container
docker stop test

# Kill the container
docker rm test

# Verify that the container is deleted (-a flag is for "all", which includes non-running containers)
docker ps -a
```

#### General Commands
```
# Start the docker daemon
$ docker -d

# Get help with Docker. Can also use –help on all subcommands
$ docker --help

# Display system-wide information
$ docker info
```

#### Images
```
# Build an Image from a Dockerfile
$ docker build -t <image_name>

# Build an Image from a Dockerfile without the cache
$ docker build -t <image_name> . –no-cache

# List local images
$ docker images

# Delete an Image
$ docker rmi <image_name>

# Remove all unused images
$ docker image prune
```

#### Containers
```
# Create and run a container from an image, with a custom name:
$ docker run --name <container_name> <image_name>

# Run a container with and publish a container’s port(s) to the host.
$ docker run -p <host_port>:<container_port> <image_name>

# Run a container in the background
$ docker run -d <image_name>

# Start or stop an existing container:
$ docker start|stop <container_name> (or <container-id>)

# Remove a stopped container:
$ docker rm <container_name>

# Open a shell inside a running container:
$ docker exec -it <container_name> sh

# Fetch and follow the logs of a container:
$ docker logs -f <container_name>

# To inspect a running container:
$ docker inspect <container_name> (or <container_id>)

#  To list currently running containers:
$ docker ps

# List all docker containers (running and stopped):
$ docker ps --all

# View resource usage stats
$ docker container stats
```
