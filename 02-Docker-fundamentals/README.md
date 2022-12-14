## What problems we have with Traditional Infra?
## Traditional Approach

1. **Installation & Configuration**
- Time consuming
- Need to perform install/configs on every server and every environment (dev, qa, staging, production)
2. **Compatibility & Dependency**
- Need to keep resolving issues related to libraries and
dependencies
3. **Inconsistencies across Environments**
- Very hard to track changes across Dev/QA/Staging and Prod environments and they end up with inconsistencies
4. **Operational Support**
- Need more resources to handle operational issues on day to day basis
    - Server Support (hardware, software)
    - Patching releases
5. **Developer Environments**
- • When a new developer joins the team, time it takes to provision his development environment in traditional approach is time taking.
<p align="center">
  <img src="https://github.com/sudheermuthyala/AKSDOCS/blob/main/02-Docker-fundamentals/2022-11-23-11-15-41.png" />
    </p>

## Physical Machines
<p align="center">
  <img src="https://github.com/sudheermuthyala/AKSDOCS/blob/main/02-Docker-fundamentals/2022-11-23-11-24-36.png" />
    </p>

## Virtual Machines
<p align="center">
  <img src="https://github.com/sudheermuthyala/AKSDOCS/blob/main/02-Docker-fundamentals/2022-11-23-11-27-02.png" />
    </p>

## Physical Machines with Docker
<p align="center">
  <img src="https://github.com/sudheermuthyala/AKSDOCS/blob/main/02-Docker-fundamentals/2022-11-23-11-30-15.png" />
    </p>

## Advantages of using Docker

## Why Containers ?
- **Flexible :** Even the most complex applications can
be containerized.
- **Lightweight :** Containers leverage and share the host kernel, making them much more efficient in terms of system resources than virtual machines.
- **Portable :** You can build locally, deploy to the cloud, and run anywhere.
- **Loosely Coupled :** Containers are highly self sufficient and encapsulated, allowing you to replace or upgrade one without disrupting others.
- **Scalable :** You can increase and automatically distribute container replicas across a datacenter.
- **Secure :** Containers apply aggressive constraints and isolations to processes without any configuration required on the part of the user.


<p align="center">
  <img src="https://github.com/sudheermuthyala/AKSDOCS/blob/main/02-Docker-fundamentals/2022-11-24-16-16-35.png" />
    </p>

## Docker Architecture

**Docker Daemon :** The Docker daemon (dockerd) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes.
 
**Docker Client :** 
- Docker client can be present on either Docker Host or any other machine.
- The Docker client (docker) is the primary way that many Docker users interact with Docker.
- When you use commands such as docker run, the client sends these commands to dockerd
(Docker Daemon), which carries them out.
- The docker command uses the Docker API.
- The Docker client can communicate with more than one daemon.

**Docker Images**
- An image is a read-only template with instructions for creating a Docker container.
- Often, an image is based on another image, with some additional customization.
- For example, we may build an image which is based on the ubuntu image, but installs the
- Apache web server and our application, as well as the configuration details needed to make
our application run.

**Docker Containers** 
- A container is a runnable instance of an image.
- We can create, start, stop, move, or delete a container using the Docker API or CLI.
- We can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.
- When a container is removed, any changes to its state that are not stored in persistent
storage disappear

<p align="center">
  <img src="https://github.com/sudheermuthyala/AKSDOCS/blob/main/02-Docker-fundamentals/2022-11-24-16-28-38.png" />
    </p>

## Verify Docker version and also login to Docker Hub
```
docker version
docker login
```

##  Pull Image from Docker Hub

```
docker pull stacksimplify/dockerintro-springboot-helloworld-rest-api:1.0.0-RELEASE
```

## Run the downloaded Docker Image & Access the Application

```
docker run --name app1 -p 80:8080 -d stacksimplify/dockerintro-springboot-helloworld-rest-api:1.0.0-RELEASE
```

## List Running Containers

```
docker ps
docker ps -a
docker ps -a -q
```

## Connect to Container Terminal
```
docker exec -it <container-name> /bin/sh
```

## Container Stop, Start
```
docker stop <container-name>
docker start  <container-name>
```

## Remove Container

```
docker stop <container-name> 
docker rm <container-name>
```

## Remove Image

```
docker images
docker rmi  <image-id>
```

## Create a new Docker Image, Run as Container and Push to Docker Hub

# Run the base Nginx container
```
docker run --name mynginxdefault -p 80:80 -d nginx
docker ps
docker stop mynginxdefault
```

 ## Create Dockerfile and copy our customized index.html
 - Dockerfile
 ```
 FROM nginx
 COPY index.html /usr/share/nginx/html
 ```
 ## Build Docker Image & run it

```
docker build -t stacksimplify/mynginx_image1:v1 .
docker run --name mynginx1 -p 80:80 -d stacksimplify/mynginx_image1:v1

Replace your docker hub account Id
docker build -t <your-docker-hub-id>/mynginx_image1:v1 .
docker run --name mynginx1 -p 80:80 -d <your-docker-hub-id>/mynginx_image1:v1
```

## Tag & push the Docker image to docker hub

```
docker images
docker tag stacksimplify/mynginx_image1:v1 stacksimplify/mynginx_image1:v1-release
docker push stacksimplify/mynginx_image1:v1-release

Replace your docker hub account Id
docker tag <your-docker-hub-id>/mynginx_image1:v1 <your-docker-hub-id>/mynginx_image1:v1-release
docker push <your-docker-hub-id>/mynginx_image1:v1-release
```

## Docker - Essential Commands
- The below are the list of essential commands we are in need 

|     Commands                 |    Description                                  |
| ------------------------------- | --------------------------------------------- |
| docker ps | List all running containers |
| docker ps -a | List all containers stopped, running |
| docker stop container-id | Stop the container which is running |
| docker start container-id | Start the container which is stopped |
| docker restart container-id | Restart the container which is running |
| docker port container-id | List port mappings of a specific container |
| docker rm container-id or name | Remove the stopped container |
| docker rm -f container-id or name| Remove the running container forcefully |
| docker pull image-info | Pull the image from docker hub repository |
| docker pull stacksimplify/springboot-helloworld-rest-api:2.0.0-RELEASE | Pull the image from docker hub repository |
| docker exec -it container-name /bin/sh | Connect to linux container and execute commands in container |
| docker rmi image-id | Remove the docker image |
| docker logout | Logout from docker hub |
| docker login -u username -p password | Login to docker hub |
| docker stats | Display a live stream of container(s) resource usage statistics |
| docker top container-id or name | Display the running processes of a container |
| docker version | Show the Docker version information |