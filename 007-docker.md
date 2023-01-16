## Docker

---

Docker is a platform for developing, shipping, and running applications in containers. Containers are lightweight, portable, and self-sufficient environments that allow developers to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package. The main benefit of using Docker is that it allows developers to create, deploy, and run applications in a consistent environment, regardless of the host operating system. This eliminates the "works on my machine" problem, where an application may work correctly on one system but not on another. It allows easy collaboration and distribution of containerized applications through the use of registries like Docker Hub.

---

### Docker Containers

Docker containers are isolated environments that run within a host operating system. They allow you to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package. Containers are lightweight, portable, and self-sufficient, which makes them well-suited for deploying and running applications in a consistent environment.

A container is created from a Docker image, which is a pre-configured environment that includes everything an application needs to run. Once you have an image, you can use the docker run command to start a new container from that image.

Here are some basic commands for working with containers:

- docker run: This command is used to start a new container from an image.
- docker start: This command starts an existing container that has been stopped.
- docker stop: This command stops a running container.
- docker ps: This command lists all running containers.
- docker rm: This command removes a container.
- docker exec: This command runs a command in a running container.

For example,

```bash
# start a new container from the ubuntu image
docker run -it ubuntu

# start an existing container
docker start my-container

# stop a running container
docker stop my-container

# list all the running containers
docker ps

# remove a container
docker rm my-container

# run command in a running container
docker exec -it my-container echo "Hello from container"
```

You can also use options like -p or -e to map a port or set environment variables, respectively, when starting a container.

A container is an isolated environment, but it can also communicate with other containers or the host machine through networks. You can connect a container to one or multiple networks, allowing it to communicate with other containers on the same network.

In summary, Docker containers are isolated environments that run within a host operating system. They are lightweight, portable, and self-sufficient, which makes them well-suited for deploying and running applications in a consistent environment. Containers are created from Docker images and can be started, stopped, listed and removed using docker commands. They are isolated environments but can communicate with other containers or the host machine through networks. Containers can also be started with options like -p or -e to map a port or set environment variables, respectively.

---

### Docker Volumes

Docker volumes are a way to manage persistent data in Docker. They allow you to separate the data of your application from the container itself, so that you can easily manage, backup, or move data without affecting the container.

A volume is essentially a directory or a file system that is stored outside of the container's filesystem, but can be mounted into the container at a specific location. Volumes can be created and managed using the docker volume command.

Here are some basic commands for working with volumes:

- docker volume create: This command creates a new volume.
- docker volume ls: This command lists all volumes on the system.
- docker volume rm: This command removes a volume.
- docker volume inspect: This command inspects the properties of a volume.

For example,

```bash
# create a new volume named my-volume
docker volume create my-volume

# list all the available volumes
docker volume ls

# remove the volume
docker volume rm my-volume
```

When you start a container, you can use the -v or --mount option to mount a volume into the container.

```bash
# start a container and mount my-volume to /app/data
docker run -v my-volume:/app/data -it ubuntu
```

It's also possible to use host paths as volumes, for example to mount a folder from the host machine into a container:

```bash
# start a container and mount host folder /data/app to /app/data
docker run -v /data/app:/app/data -it ubuntu
```

Docker volumes can also be used with docker-compose to manage the volumes in a multi-container application. You can specify the volumes in the docker-compose.yml file and use docker-compose up command to create and start the containers with the defined volumes.

In summary, Docker volumes provide a way to manage persistent data in Docker by allowing you to separate the data of your application from the container itself. It enables you to easily backup, move or share data between containers, and also provides a way to persist data even if the container is deleted.

---

### Docker Networks

Docker networks are a way to manage the communication between containers in a Docker environment. They allow you to create isolated networks for your containers, and control how the containers communicate with each other and with the host.

Docker provides several types of networks, including bridge, host, and overlay networks.

- Bridge networks are the default type of network in Docker. They allow containers on the same network to communicate with each other, but not with the host or other networks.
- Host networks use the host's networking stack, so the containers use the host's IP address and ports, and can communicate with the host and other networks.
- Overlay networks allow you to connect multiple Docker daemons together and create a virtual network that spans across multiple hosts.

Here are some basic commands for working with networks:

- docker network create: This command creates a new network.
- docker network ls: This command lists all networks on the system.
- docker network rm: This command removes a network.
- docker network connect: This command connects a container to a network.
- docker network disconnect: This command disconnects a container from a network.

For example,

```bash
# create a new bridge network named my-network
docker network create --driver bridge my-network

# list all the available networks
docker network ls

# remove the network
docker network rm my-network

# start a container and connect it to my-network
docker run --network my-network --name my-container -it ubuntu
```

You can also connect multiple container to the same network and they can communicate with each other using the container name or IP addresses.

```bash
# start another container and connect it to my-network
docker run --network my-network --name my-container2 -it ubuntu

# check the container ip address
docker inspect my-container

# test the communication between the containers
docker exec -it my-container ping my-container2
```

In summary, Docker networks are a way to manage the communication between containers in a Docker environment. They allow you to create isolated networks for your containers and control how the containers communicate with each other and with the host. Docker provides several types of networks, including bridge, host, and overlay networks. The docker network commands allows you to create, manage and inspect the networks. By connecting the containers to the same network, they can communicate with each other using the container name or IP addresses.

---

### Docker Images

Docker images are the building blocks of containerized applications in Docker. An image is a pre-configured environment that includes all the necessary files, libraries, and dependencies for an application to run.

An image is created from a Dockerfile, which is a script that contains instructions for building the image. The Dockerfile is used by the docker build command to create the image. Once an image is created, it can be used to start one or more containers, which are running instances of that image.

Here are some basic commands for working with images:

- docker pull: This command is used to download an image from a registry, such as Docker Hub.
- docker push: This command is used to upload an image to a registry.
- docker images: This command lists all images that are currently on the system.
- docker rmi: This command removes an image.

An example of creating an image

```bash
# create a new file named Dockerfile in your application directory with the following content
# FROM python:3.8
# COPY . /app
# WORKDIR /app
# RUN pip install -r requirements.txt
# CMD ["python", "app.py"]

# Build the image
docker build -t my-app .
```

This command will build an image from the Dockerfile in the current directory, and tag it as my-app.

Once the image is built, it can be used to start a container

```bash
docker run my-app
```

Docker Hub is the default public registry for images. It's a centralized repository for storing and sharing images that allows for easy collaboration and distribution of containerized applications. Developers can also use other registries like quay.io, gcr.io, and others.

Docker images are also versioned, meaning that you can have multiple versions of the same image, each with a unique tag. For example, you can have an image named my-app with the tag 1.0 and another image named my-app with the tag 2.0. This allows you to easily roll back or upgrade to a different version of an image.

In summary, Docker images are the building blocks of containerized applications in Docker. They are pre-configured environments that include all the necessary files, libraries and dependencies for an application to run. These images can be created from a Dockerfile and can be used to start one or more containers. They can be stored and shared using the Docker Hub, and other registries, and also versioned to allow for easy rollback or upgrade to a different version of an image.

---

### Docker Registries

Docker registries are centralized repositories for storing and distributing Docker images. They provide a way to manage, share and distribute Docker images to different environments and users.

Docker Hub is the default public registry for images. It's a free, centralized repository for storing and sharing images that allows for easy collaboration and distribution of containerized applications. Developers can also use other registries like quay.io, gcr.io, and others.

Docker registries can be either public or private. Public registries, like Docker Hub, allow anyone to search for, download, and use images. Private registries, on the other hand, are restricted to specific users or teams, and require authentication to access.

To use a Docker registry, you will need to log in and authenticate with the registry using the docker login command. Once you are logged in, you can use the docker pull and docker push commands to download and upload images to the registry.

Here are some basic commands for working with registries:

- docker login: This command is used to log in to a registry.
- docker logout: This command is used to log out of a registry.
- docker pull: This command is used to download an image from a registry.
- docker push: This command is used to upload an image to a registry.

For example,

```bash
# log in to the Docker Hub
docker login

# pull an image from the Docker Hub
docker pull ubuntu

# tag an image and push to the Docker Hub
docker tag my-app:latest myusername/my-app:1.0
docker push myusername/my-app:1.0
```

You can also use docker-compose to specify the registry in the docker-compose.yml file and push and pull the images from the specific registry.

In summary, Docker registries are centralized repositories for storing and distributing Docker images. They provide a way to manage, share and distribute Docker images to different environments and users. Docker Hub is the default public registry, but developers can also use other registries like quay.io, gcr.io and others. They can be either public or private, and requires authentication to access. The docker login, docker pull and docker push commands are used to interact with the registries.

---

### Docker Compose

Docker Compose is a tool for defining and running multi-container applications with Docker. It allows you to define the services that make up your application in a single docker-compose.yml file, and then start, stop, and manage those services with a single docker-compose command.

A docker-compose.yml file is a YAML file that defines the services, networks and volumes for your application. Each service is defined with its own configuration options, such as the image to use, environment variables to set, and ports to expose.

Here are some basic commands for working with Docker Compose:

- docker-compose up: This command starts the services defined in the docker-compose.yml file.
- docker-compose down: This command stops and removes the containers, networks, and volumes defined in the docker-compose.yml file.
- docker-compose ps: This command lists the running containers created by docker-compose.
- docker-compose exec: This command runs a command in a running container.
- docker-compose logs: This command shows the logs of the containers.

An example of docker-compose.yml file:

```bash
version: '3'
services:
  web:
    build: .
    ports:
     - "8000:8000"
    volumes:
     - "./web:/web"
  db:
    image: postgres
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
    ports:
     - "5432:5432"
    volumes:
     - "db-data:/var/lib/postgresql/data"
volumes:
  db-data:
```

This file defines two services web and db, the web service is built from the current directory and the db service is using the postgres image. It also maps the ports and volumes for each service.

You can use the docker-compose up command to start the services defined in this file

```bash
docker-compose up
```

You can also scale the number of instances of a service using the docker-compose up --scale command

```bash
docker-com
```

---

### Dockerfile

A Dockerfile is a script that contains instructions for building a Docker image. It is used by the docker build command to create an image from a set of instructions. Each instruction in a Dockerfile creates a new layer in the image.

A Dockerfile typically starts with a base image, such as FROM ubuntu:18.04, and then runs a series of instructions to install dependencies, copy files, and configure the environment.

Here are some examples of common instructions used in a Dockerfile:

- `FROM`: This instruction specifies the base- image for the build. For example, FROM ubuntu:18.04 specifies that the image should be based on the latest version of Ubuntu 18.04.

- `RUN`: This instruction runs a command in the container. For example, RUN apt-get update && apt-get install -y nginx installs Nginx on the container.

- `COPY`: This instruction copies files or directories from the host to the container. For example, COPY . /app copies the current directory to the /app directory in the container.

- `ENV`: This instruction sets an environment variable in the container. For example, ENV PORT 80 sets the PORT environment variable to 80.

- `EXPOSE`: This instruction specifies which ports the container will listen on. For example, EXPOSE 80 specifies that the container will listen on port 80.

- `CMD`: This instruction specifies the command that will be run when the container starts. For example, CMD ["nginx", "-g", "daemon off;"] starts Nginx in the container.

Here's an example of a simple Dockerfile that creates an image for a web server:

```bash
FROM ubuntu:18.04

# update and install nginx
RUN apt-get update && apt-get install -y nginx

# copy the web files
COPY . /var/www/html

# expose port 80
EXPOSE 80

# start nginx
CMD ["nginx", "-g", "daemon off;"]
```

This Dockerfile starts with the ubuntu:18.04 image, installs Nginx, copies the web files to the container, expose port 80 and starts Nginx.

To build the image, you can use the docker build command and specify the path to the Dockerfile

```bash
docker build -t my-web-server .
```
