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
# Download images from remote registries (default is Docker Hub)
docker pull

# List local images
$ docker images

# Metadata for an image (image must exist locally)
docker inspect <image_name>

# Inspect the manifest list of images stored in registries
# (images do not have to exist locally)
docker manifest inspect <image_name>

# Build an Image from a Dockerfile. Trailing '.' makes `pwd` the **build context**
$ docker build -t <image_name> .

# Build an Image from a Dockerfile without the cache
$ docker build -t <image_name> . –no-cache

# Delete an Image
$ docker rmi <image_name>

# Remove all unused images
$ docker image prune

# Docker CLI plugin that works with latest build engine features
# As of Aug-2024, this is what you use with the --platform flag to
# get images from platforms other than the local plaform
# (AMD on an Mx MacOS)
docker buildx ...

# Docker CLI plugin to do image vulnerability scanning
docker scout ...
```

#### Containers
```
# Create and run a container from an image, with a custom name:
docker run --name <container_name> <image_name>

# Run a container from an image and remove the container when it stops
docker run --rm <image>

# Run a container with and publish a container’s port(s) to the host.
docker run -p <host_port>:<container_port> <image_name>

# Run a container in the background
docker run -d <image_name>

# Start or stop an existing container:
docker start|stop <container_name> (or <container-id>)

# Restart a stopped container (not sure how this is different than start):
docker restart <container_name>

# Attach your shell to the above container (named 'test')
docker attach test

# Exit a container without killing the process you're attached to 
Ctrl PQ

# Remove a stopped container:
docker rm <container_name>

# Remove a container without stopping it first:
docker rm <container_name> -f

# Open a shell inside a running container:
docker exec -it <container_name> sh

# Run top inside a container:
docker exec -it <container_name> top

# Fetch and follow the logs of a container:
docker logs -f <container_name>

# To inspect a running container:
docker inspect <container_name> (or <container_id>)

#  To list currently running containers:
docker ps

# List all docker containers (running and stopped):
docker ps --all
docker ps -a

# View resource usage stats
$ docker container stats

# Docker debug (requires subscription $$$)
docker debug
```

#### Docker Compose
```
# Start containers specified in the default compose.yaml file in the current dir
docker compose up

# Start containers (default compose.yaml) and detach
docker compose up -d

# Stop containers (default compose.yaml)
# This does NOT remove the containers
docker compose stop

# Stop and remove containers (default compose.yaml)
# Removes containers, but not volumes or images by default (flags exist, see next)
docker compose down

# Stop containers and remove everything from the compose.yaml specs
docker compose down --volumes --rmi all

# See all running containers from a Compose app
docker compose ps

# See all containers (running or not) from a Compose app
docker compose ps -a

# Build images before starting the containers
docker compose up --build

# Start containers with a non-default yaml file
docker compose -f example-app/my-app.yml up
```
