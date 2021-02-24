# About Docker
1) Docker is an open-source project that automates the development, deployment and running of applications inside isolated containers. Containers allow developers to bundle up an application with all of the parts it needs, such as libraries and other dependencies, and ship it as one package.
2) Docker is both a daemon (a process running in the background) and a client command. It’s like a virtual machine but it’s different in important ways. First, there’s less duplication. With each extra VM you run, you duplicate the virtualization of CPU and memory and quickly run out resources when running locally. Docker is great at setting up a local development environment because it easily adds the running process without duplicating the virtualized resource. Second, it’s more modular. Docker makes it easy to run multiple versions or instances of the same program without configuration headaches and port collisions. Try that in a VM!
3) If you think of Docker as a virtual machine or a Vagrant machine, you might want to cram a lot of things in it (e.g., services, monitoring software and your application). That would be a mistake. You don’t put many things into a Docker image; instead, you use many Docker containers to achieve the full stack.
4) There are a dozen reasons to use Docker. I’ll focus here on three: consistency, speed and isolation. By consistency, I mean that Docker provides a consistent environment for your application from development all the way through production — you run from the same starting point every time. By speed, I mean you can rapidly run a new process on a server. Because the image is preconfigured and installed with the process you want to run, it takes the challenge of running a process out of the equation. By isolation, I mean that by default each Docker container that’s running is isolated from the network, the file system and other running processes.
5) When you have your application in a Docker container, you can be sure that the code you’re testing locally is exactly the same build artifact that goes into production. There are no changes in application runtime environments. That makes Docker an exceptional tool all the way from development through production.
6) Eliminate the “it works on my machine” problem once and for all. One of the benefits that the entire team will appreciate is parity. Parity, in terms of Docker, means that your images run the same no matter which server or whose laptop they are running on. For your developers, this means less time spent setting up environments, debugging environment-specific issues, and a more portable and easy-to-set-up codebase. Parity also means your production infrastructure will be more reliable and easier to maintain.

## Docker Daemon
The Docker daemon (dockerd) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.

## Docker Client
The Docker client (docker) is the primary way that many Docker users interact with Docker. When you use commands such as docker run, the client sends these commands to dockerd, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.

## Docker Images
1) An image is a read-only template with instructions for creating a Docker container. Often, an image is based on another image, with some additional customization. For example, you may build an image which is based on the ubuntu image, but installs the Apache web server and your application, as well as the configuration details needed to make your application run.
2) You might create your own images or you might only use those created by others and published in a registry. To build your own image, you create a Dockerfile with a simple syntax for defining the steps needed to create the image and run it. Each instruction in a Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt. This is part of what makes images so lightweight, small, and fast, when compared to other virtualization technologies.

## Docker Containers
1) A container is a runnable instance of an image. You can create, start, stop, move, or delete a container using the Docker API or CLI. You can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.
2) By default, a container is relatively well isolated from other containers and its host machine. You can control how isolated a container’s network, storage, or other underlying subsystems are from other containers or from the host machine.
3) A container is defined by its image as well as any configuration options you provide to it when you create or start it. When a container is removed, any changes to its state that are not stored in persistent storage disappear.

## Building a Docker Image

### Method 1 
1) Pull a base image from docker hub, 
2) Run a container from the image
3) Run docker exec to access the container shell and install all the libraries and dependencies dependencies
4) Run docker commit to save the container as an image

### Method 2
1) Use a Dockerfile to build the required image with all the requirements

```Suggested way is: Method 2```

**With method 1**, The final generated image has to be uploaded to a registry and needs to be pulled whenever it needs to be used. Whereas with method 2, all we need is a Dockerfile with the required commands, and we can generate the image on any system.

**With method 2**, each step is created as an intermediate layer which is cached. So when one step changes any steps before that step don’t have to be rerun

**Using method 2** is a more automated method of doing it, especially if the process needs to be repeated with only slight modifications. Method 1 would need everything to be done all over again.



## Docker Development Best Practices
The following development patterns have proven to be helpful for people building applications with Docker. If you have discovered something we should add, let us know.

### Ways to keep the images small
1) Small images are faster to pull over the network and faster to load into memory when starting containers or services. There are a few rules of thumb to keep image size small:

2) Start with an appropriate base image. For instance, if you need a JDK, consider basing your image on the official openjdk image, rather than starting with a generic ubuntu image and installing openjdk as part of the Dockerfile.

3) Use multistage builds. For instance, you can use the maven image to build your Java application, then reset to the tomcat image and copy the Java artifacts into the correct location to deploy your app, all in the same Dockerfile. This means that your final image doesn’t include all of the libraries and dependencies pulled in by the build, but only the artifacts and the environment needed to run them.

4) If you need to use a version of Docker that does not include multistage builds, try to reduce the number of layers in your image by minimizing the number of separate RUN commands in your Dockerfile. You can do this by consolidating multiple commands into a single RUN line and using your shell’s mechanisms to combine them together. Consider the following two fragments. The first creates two layers in the image, while the second only creates one.
```
        RUN apt-get -y update
        RUN apt-get install -y python
```
```
        RUN apt-get -y update && apt-get install -y python
```

5) If you have multiple images with a lot in common, consider creating your own base image with the shared components, and basing your unique images on that. Docker only needs to load the common layers once, and they are cached. This means that your derivative images use memory on the Docker host more efficiently and load more quickly.

6) To keep your production image lean but allow for debugging, consider using the production image as the base image for the debug image. Additional testing or debugging tooling can be added on top of the production image.

7) When building images, always tag them with useful tags which codify version information, intended destination (prod or test, for instance), stability, or other information that is useful when deploying the application in different environments. Do not rely on the automatically-created latest tag.

### Where and how to persist application data
1) Avoid storing application data in your container’s writable layer using storage drivers. This increases the size of your container and is less efficient from an I/O perspective than using volumes or bind mounts.
2) Instead, store data using volumes.
3) One case where it is appropriate to use bind mounts is during development, when you may want to mount your source directory or a binary you just built into your container. For production, use a volume instead, mounting it into the same location as you mounted a bind mount during development.
4) For production, use secrets to store sensitive application data used by services, and use configs for non-sensitive data such as configuration files. If you currently use standalone containers, consider migrating to use single-replica services, so that you can take advantage of these service-only features.
 
 ### Suggestions and Guidelines
1) Use Dockerfiles and docker build to create images.
2) Create different images for different components in the application stack. This will make it easier when we need to deploy them across multiple servers. It also helps make scalability easier, since we can just increase the number of container replicas for only modules that are needed.
3) Keep the containers isolated. Do not expose ports outside the container if they don’t need to be accessed by the host system. Use bridge networks to allow communication between containers when needed. 
4) Use volumes to share files between containers or between container and host only when it is really necessary.
5) Volumes should only be used for data and not for code.
6) Volumes should be used for data that needs to be kept persistent. Such as models or DB data, because stopping the container will result in loss of the data inside the container.
7) Use docker compose to define all the services/modules of the app, along with the volumes, networks, and any other options that need to be configured for the images and containers. This makes managing them and starting and stopping them much more easier and convenient, as well as easy to use with little knowledge of docker.
8) Try to use base images that are available for required modules on docker hub. For example, Node, Python, Anaconda, Elasticsearch, etc. Instead of taking an OS base image and installing everything from scratch.
9) It is recommended to use base images that use alpine OS, because they’re lightweight, leading to smaller docker images and containers.
10) Put steps that are more likely to change, such as commands to copy code, towards the end of the Dockerfile, so that rebuilding uses as many caches layers of images as possible and it’s much faster.



## Docker Cheat Sheet

### Build
1) Build an image from the Dockerfile in the current directory and tag the image
``` 
        docker build -t myimage:1.0 .
```

2) List all images that are locally stored with the Docker Engine
``` 
        docker image ls
```
3) Delete an image from the local image store
```
        docker image myimage:1.0
```
4) Create a container
```
        docker create --name <container_name> <image_name>
```
### Share
1) Pull an image from a registry
```
        docker pull myimage:1.0 
```
2) Retag a local image with a new image name and tag
```
        docker tag myimage:1.0 myrepo/myimage:2.0  
```
3) Push an image to a registry 
```
        docker push myrepo/myimage:2.0
```
4)Add contents to existing running container
```
        docker cp <file_name> <container_name>:<file_path_inside_container>
```

### Run
1) Run a container from the Alpine version 3.9 image, name the running container “anyname” and expose port 5000 externally, mapped to port 80 inside the container.
```
        docker container run --name anyname -p 5000:80 alpine:3.9
```
2) Start an existing continer:
```
        docker start <container_name>
```

### Docker Management

1)  Remove tagged image
```
        docker rmi <repo_name>:<tag_name>
```
2) Check the volumes list
```
        docker volume ls
```
3) Going inside the conatiner
```
    docker exec -it <containerID> bash
```
4) Delete all running and stopped containers (Use carefully) 
```
        docker container rm -f $(docker ps -aq)
```
5) Stop a running container through SIGTERM 
```
        docker container stop anyname
```
6) Stop a running container through SIGKILL 
```
        docker container kill anyname
```
7) List the networks 
```
        docker network ls
```
8) List the running containers (add --all to include stopped containers) 
```
        docker container ls
```
9) Print the last 100  lines of a container’s logs 
```
        docker logs --tail 100 containerID
```

All commands below are called as options to the base docker command. Run docker <command> --helpfor more information on a particular command.

```
app                     Docker Application

assemble                Framework-aware builds (Docker Enterprise)
builder                 Manage builds 
cluster                 Manage Docker clusters (Docker Enterprise)
config                  Manage Docker configs
context                 Manage contexts 
engine                  Manage the docker Engine
image                   Manage images
network                 Manage networks
node                    Manage Swarm nodes
plugin                  Manage plugins
registry                Manage Docker registries
secret                  Manage Docker secrets
service                 Manage services 
stack                   Manage Docker stacks
swarm                   Manage swarm    
system                  Manage Docker
template                Quickly scaffold services (Docker Enterprise) 
trust                   Manage trust on Docker images
volume                  Manage volumes
```

#### For more comprehensive command list please check:
- https://phoenixnap.com/kb/list-of-docker-commands-cheat-sheet
- http://dockerlabs.collabnix.com/docker/cheatsheet/


## Docker-Compose 
Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration. To learn more about all the features of Compose, see the list of features.

Compose works in all environments: production, staging, development, testing, as well as CI workflows. You can learn more about each case in Common Use Cases.

Using Compose is basically a three-step process:

Define your app’s environment with a Dockerfile so it can be reproduced anywhere.

Define the services that make up your app in docker-compose.yml so they can be run together in an isolated environment.

Run docker-compose up and Compose starts and runs your entire app.

A docker-compose.yml looks like this:
```
#docker-compose.yml
version: '2.0'
services:
  web:
    build: .
    ports:
    - "5000:5000"
    volumes:
    - .:/code
    - logvolume01:/var/log
    links:
    - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```
### Features
1) Multiple isolated environments on a single host
2) Preserve volume data when containers are created
3) Only recreate containers that have changed
4) Variables and moving a composition between environments

### Commands 
```
#default runs the content of docker-compose.yml
docker-compose start
docker-compose stop
docker-compose pause
docker-compose unpause
docker-compose ps
docker-compose up -d   (-d is for detached mode)
docker-compose down
```
```
# if have to run docker-compose command from other file than docker-compose.yml
docker-compose -p <NAMES> -f docker-compose.yml -f docker-compose-test.yml up -d
docker-compose -p <NAMES> -f docker-compose.yml -f docker-compose-test.yml down
```
```
#if build is mentioned in docker-compose.yml then command to build an image
sudo docker-compose build <containername>
```
### Reference

#### 1)  **Building**
```
<containername>:
  # build from Dockerfile
  build: .
  args:     # Add build arguments
    APP_HOME: app
    
  # build from custom Dockerfile
  build:
    context: ./dir
    dockerfile: Dockerfile.dev
    
  # build from image
  image: ubuntu
  image: ubuntu:14.04
  image: tutum/influxdb
  image: example-registry:4000/postgresql
  image: a4bc65fd
```
#### 2)  **Ports**
```
  ports:
    - "3000"
    - "8000:80"  # host:container
  # expose ports to linked services (not to host)
  expose: ["3000"]
```
#### 3)  **Networks**
```
# creates a custom network called `frontend`
networks:
  frontend:
```
#### 4)  **Volumes**
```
# Mount host paths or named volumes, specified as sub-options to a service
  db:
    image: postgres:latest
    volumes:
      - "/var/run/postgres/postgres.sock:/var/run/postgres/postgres.sock"
      - "dbdata:/var/lib/postgresql/data"

volumes:
  dbdata:
```

#### For Complete information look at 
- https://docs.docker.com/compose/
- https://devhints.io/docker-compose


## Do's and Don'ts of Docker

1) Don’t install stuff inside a running container. Put it in the Dockerfile.
2) Don’t pull from version control into containers. Instead build a container that contains your app.
3) Don’t keep containers running for a long time without security updates. Build a fresh one regularly.
4) Don’t just expose ports as for instance 8000:8000, as docker exposes them on 0.0.0.0 by default, so also on all your server’s external interfaces. The basic “ufw” won’t work, as Docker opens up those ports with iptables anyway. So explicitly open them up on 127.0.0.1.
5) Don’t store data in containers.
6) Don’t use a single layer image.
7) Don’t create images from running containers.
8) Don't use --force or -f options with docker command until absolutely sure of it.
9) Don't just run a docker command without understanding what it does.
10) Don’t use only the “latest” tag.
11) Don’t store credentials in the image. Use environment variables.
12) Don’t run more than one process in a single container.
13)  Don’t run processes as a root user.
14) Don't think Docker will solve all your (DevOps) problems.
15) Use caching properly for your Dockerfiles.
16) Maintain your containers in a registry.
17) Plan your containers life-cycles.
18) Log all the things
19) Define a proper start logic.
20) Learn how to set up your containers as cattle (something wrong, just grab a new one) !!! They are disposable. They should be created and disposed off without a second thought.
