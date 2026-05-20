# Docker
<!-- MarkdownTOC -->

- [Introduction](#introduction)
- [Dockerfile](#dockerfile)
    - [Images](#images)
    - [Containers](#containers)
        - [Interacting with a running container](#interacting-with-a-running-container)
    - [Volumes](#volumes)
    - [Dockerignore](#dockerignore)
- [Docker Compose](#docker-compose)
    - [Installation](#installation)
    - [Compose File](#compose-file)
    - [Compose Commands](#compose-commands)
- [Notes During Cloud Jam](#notes-during-cloud-jam)
- [GCloud Commands](#gcloud-commands)
- [Tips and Tricks](#tips-and-tricks)
    - [show the run command of a docker container](#show-the-run-command-of-a-docker-container)
- [Run commands for containers I removed](#run-commands-for-containers-i-removed)

<!-- /MarkdownTOC -->

# Introduction
A Docker container is different from a virtual machine in that it shares the OS kernel with the host system and only adds the essential binaries on top of that. Therefore, a container starts faster and uses less resources.

A _container_ is running instance of an _image_. An _image_ is a template for creating the desired environment, a snapshot of the system at a given time.

Images are defined using a _docker file_, which is a list of steps to perform to create an image.

# Dockerfile
A Dockerfile is a blueprint to build a docker image, which can be based on an existing image.
The instruction format of the Dockerfile is `INSTRUCTION arguments`. The instruction is not case-sensitive. However, the convention is for them to be UPPERCASE to distinguish them from arguments more easily.

```bash
# Dockerfile
# The file must start with a FROM instruction which specifies the base image
FROM image_name:version
FROM ubuntu:14.04

# Create and set the working directory for RUN, CMD, ENTRYPOINT, COPY and ADD.
# It can be used multiple times.
# If a relative path is provided, it will be relative to the path of the previous WORKDIR instruction.
WORKDIR /usr/src/app

# Copy a file from host to the image
# <src> MUST be within the build context.
# If <src> is a directory, the entire contents of the directory are copied, including filesystem metadata.
# If <src> is a directory, the directory itself is not copied, just its contents.
# If <dest> doesn’t exist, it is created along with all missing directories in its path.
COPY <src relative to build context> <dst: absolute path or relative to WOKRDIR>
COPY src/ /var/www/html
COPY src/ ./

# ADD is the same as COPY in additoin to allowing URLs and untaring tar files.
# It is recommended to use COPY over ADD for its more intuitive behaviour.
# The source MUST be within the build context
ADD <src> <dst>

# Tell the container to listen on a port. Default port type is TCP.
EXPOSE 80

# Set environment variables
ENV VARNAME value
ENV PATH ${PATH}:/usr/local

# Execute a command on top of the current image and commit the result.
RUN cmd

# ENTRYPOINT specifies a command that will always be executed when the container runs.
# Default entrypoint is ["/bin/sh -c"]
ENTRYPOINT ["executable", "param1", "param2"]
ENTRYPOINT command param1 param2
ENTRYPOINT ["go"]

# CMD specifies arguments that will be fed to the ENTRYPOINT.
# There is no default CMD.
# There can't be more than one CMD.
CMD [ "npm", "run", "dev" ]
```

__.dockerignore__
Contains files and folders that would be ignored by the commands in the Dockerfile such as COPY.

## Images
An image is an imputable snapshot of an OS environment.

```bash
# Pull an image and store it locally
# Not specifying a tag would pull :latest
docker pull image_name[:tag]
# Create an image from a dockerfile
docker build [-t image_name[:tag]] [-f docker_file(default:PATH/Dockerfile)] build_context
docker build -t ditek/my-proxy:v1.0 .
docker build -t my-image .
```

## Containers
A container is a running process created from an image.

```sh
# Create a container from an image without running it. Same options as run.
docker create [OPTIONS] IMAGE [COMMAND] [ARG...]
    --name my-container           # Assign a name to reference the container later
    --tty , -t                    # Allocate a pseudo-TTY to allow interacting with the container
# Start a previously created container.
docker start  [OPTIONS] CONTAINER
    --interactive , -i
    --attach , -a                 # Attach STDOUT/STDERR and forward signals

# Run an image (create + start)
docker run \
        -p port_host:port_container \  # Map a port from host to container
        -v dir_host:dir_container \  # Map a host directory to a container folder
        -v $(pwd)/src:/src  \
        --rm \                      # remove all container data between executions
        -d \                        # Run in the background
        --tty -t \                  # connect stdin and stdout to our process, including signals such as CTRL+C
        --interactive -i \          # required with --tty option. Keep STDIN open.
        --name <container-name> \   # Set a name for the container
        image_name
docker run -p 4000:80 my_image      # Run and forward port 4000 from host to port 80 in the container
docker run -d my_image              # Run in the background
docker run -v /tmp/src/:/var/src    # Mount a folder from host inside the container
docker run -v $(pwd):/root -it \
        my_image /bin/bash          # Run an image, map current dir, run bash

# Commit a container's state to an image
docker commit my-container my-image

# Examples
docker run --rm -it my-image
```

### Interacting with a running container
```sh
docker start my-container           # Start the container
docker stop my-container            # Stop the container
docker kill my-container            # Kill (force stop) the container
docker rm my-container              # Remove a stopped container

# Show used resources by containers
docker stats

docker logs [container_id/name]          # Look at the logs
docker logs -f [container_id/name]       # Follow the logs
docker logs -t n [container_id/name]     # Tail the logs showing last n lines

docker exec -it [container_id/name] bash     # Start interactive (-it) bash inside a running container

docker inspect [container_id]       # Examine container's metadata (args, creation date, etc.) in JSON format

# Container operations
docker ps                           # Show running containers
docker ps -q                        # Show running containers' ids
docker ps -a                        # Show all containers
docker ps -are                      # Show containers that are running or has run before
docker stop $(docker ps -q)         # Stop all running containers
docker rm $(docker ps -aq)          # Remove all containers

# Image operations
docker rmi [image_name_or_id]       # Remove image
docker rmi $(docker images -aq)     # Remove all images
docker image prune                  # Remove unused or dangling images

# Sharing devices
--device=[]
      Add a host device to the container (e.g. --device=/dev/sdc:/dev/xvdc:rwm)
```

## Volumes
_Volumes_ are used to share a directory between the host and the container or between different containers.

```sh
docker volume create 
```

## Dockerignore
User to get Docker to ignore some files.

__IMPORTANT__

If you are working with nodejs, make sure to ignore `node_modules`:

```sh
# .dockerignore
node_modules
```

---------------------------------------
# Docker Compose
Compose is a tool for defining and running multi-container Docker applications using a YAML file to configure your application's services.

## Installation
As of Jun 2023, the `docker-compose` command has been deprecated in favor of the `compose` plugin.

```sh
sudo apt-get install docker-compose-plugin
```

## Compose File
The default path for a Compose file is `compose.yaml` (preferred) or `compose.yml`, `docker-compose.yaml`, `docker-compose.yml` that is placed in the working directory.

Each key in the `services` object represents a different container.

```yaml
version: "3"
services:
  # Container name
  reverseproxy:
    # Option 1: Using an existing dockerfile
    # Path to the working directory where the dockerfile is located
    build: .
    # Option 2: specifying the image to base on
    image: ditek/reverseproxy
    ports:
      - 8080:8080
    restart: always
    depends_on:
     - backend-user
  backend-user:
   image: ditek/udacity-restapi-user
   # Mapping a volume or a host directory to a container directory
   volumes:
    # From a directory
    - $HOME/.aws:/root/.aws
    # From a defined volume. Mount it to /foo
    - db-data: /foo
   environment:
    ENV_VARIABLE: $DB_USERNAME
    URL: "http://localhost:8100"
  frontend:
   image: ditek/udacity-frontend
   ports:
    - "8100:80"

# Define folumes here
volumes:
  - db-data:
```

`docker-compose-build.yaml`

```yaml
version: "3"
services:
 reverseproxy:
  build:
   context: .
  image: ditek/reverseproxy
 backend_user:
  build:
   context: ../../udacity-c3-restapi-user
  image: ditek/udacity-restapi-user
 frontend:
  build:
   context: ../../udacity-c3-frontend
  image: ditek/udacity-frontend:local
```

## Compose Commands
```sh
# Build the images for each of our defined services, using the command:
docker compose -f docker-compose-build.yaml build --parallel

# Find the compose file in the current directory and run the containers.
# Runs in attached mode (foreground)
docker compose up
# Run in detached mode (background)
docker compose up -d

# Shutdown the containers
docker compose down

# Show running containers
docker compose ps
```

---------------------------------------
# Notes During Cloud Jam
```bash
# Specify docker container name when running an image
docker run --name [container-name] hello-world

# Build an image with a tag
# (if the tag isn't specified, the image sill have the tag 'latest')
docker build -t node-app:0.1 .
```

---------------------------------------
# GCloud Commands
```bash
# List the active account name
gcloud auth list

# List project ID
gcloud config list project

# Create a cluster
gcloud container clusters create \
                <CLUSTER-NAME> \
                --num-nodes 2 \
                --machine-type n1-standard-1 \
                --zone us-central1-a

# Get authentication credentials for the cluster
gcloud container clusters get-credentials <CLUSTER-NAME>

# Delete a cluster
gcloud container clusters delete <CLUSTER-NAME>
```

---------------------------------------

# Tips and Tricks

## show the run command of a docker container
```sh
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock:ro assaflavie/runlike CONTAINER_ID
```

# Run commands for containers I removed
```sh
docker run --name=adoring_banach --hostname=89925f53f26d --volume /Volumes/Seagate/git/EmuELEC:/EmuELEC --network=bridge --runtime=runc -t bitnami/minideb /bin/bash
```

