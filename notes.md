docker 
docker image
ec2
ecs

Frontend (npm run build) will create three filesof[html,css,js] copy these files to public folder of backend project. Then, create a Dockerfile in the backend project root directory with the following content:

docker build . -t backend(tag name)
docker run backend-image
docker run -p 4000:3000 backend


what is devops?
sof dev + IT ops

Q) what is dockers?Why do we need it?
Docker is a platform that allows developers to automate the deployment of applications inside lightweight, portable containers. Containers package an application and its dependencies together, ensuring that it runs consistently across different environments.

Q) Docker images and containers?
Docker images are read-only templates that contain the application code, libraries, and dependencies needed to run an application. Containers are instances of Docker images that can be executed, providing an isolated environment for the application to run.
Q)Difference between Docker images and containers:
- Docker Image: A Docker image is a static snapshot of an application and its dependencies. It is used to create containers. Images are built from a Dockerfile and can be versioned and shared.
- Docker Container: A Docker container is a running instance of a Docker image. It is an isolated environment that runs the application and can be started, stopped, and deleted. Containers are lightweight and can be easily moved between different environments.

docker run -it ubuntu
if not present in local system it will pull from docker hub and run the container.
-it -> intractive terminal

docker --v  -->  to check version
docker --> to print all docker commands

docker pull <image_name>  --> to pull image from docker hub

docker images  --> to list all images present in local system

docker run <image_name>  --> to run a container from the specified image

docker run -it <image_name>  --> to run a container in interactive mode with a terminal(input and output)

docker ps  --> to list all running containers

docker ps -a  --> to list all containers (running and stopped)

docker stop <container_id> or <container_name> --> to stop a running container

docker start <container_id> or <container_name> --> to start a stopped container

docker rmi <image_id> or <image_name> --> to remove a Docker image from the local system

docker rm <container_id> or <container_name> --> to remove a stopped container from the local system

docker pull <image_name>  --> to pull a image from Docker Hub

docker pull <image_name>:version  --> to pull a specific version of an image from Docker Hub

detach mode: docker run -d <image_name>  --> to run a container in detached mode (in the background)

by deafult, docker run command runs the container in attached mode, which means that the terminal is attached to the container's standard input/output streams. In detached mode, the container runs in the background and does not block the terminal.

attach mode: docker attach <container_id>  --> to attach to a running container and view its output

Docker images layers

container layer
  ^
  |
layer 2 (Read only)
  ^
  |
layer 1 (Read only)
  ^
  |
base layer (Read only)

If i have an two image of same application with different versions then some layers are common between them.

Port binding 
Host machine and port machine(containers) ports are different
we have to bind it.
docker run -p8080:3306 <image_name>  --> to bind port 8080 on the host machine to port 3306 in the container

docker exec -it mysql-latest /bin/bash
command can run inside the container to get into the bash shell of the running container.
exit does not stop the container.

Yes! You can set up Docker containers using both CLI commands and Docker YAML files. Both approaches are officially supported and documented by Docker.

The YAML approach uses Docker Compose, which is particularly useful when your application has multiple services, such as Node.js, MongoDB, Redis and frontend.

Method 1: Docker CLI
Imperative approach
You tell Docker exactly what commands to execute.
docker network create mongo-network

docker run -d \
  -p 27017:27017 \
  --name mongo \
  --network mongo-network \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=qwerty \
  mongo


Method 2: Docker Compose (YAML)
Declarative approach
You describe the desired infrastructure in a configuration file.
services:
  mongo:
    image: mongo:latest

    container_name: mongo

    ports:
      - "27017:27017"

    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: qwerty

    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
  

we have setup mongodb and mongodb express

docker run -d `
  -p 8081:8081 `
  --name mongo-express `
  --network mongo-network `
  -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin `
  -e ME_CONFIG_MONGODB_ADMINPASSWORD=qwerty `
  -e ME_CONFIG_MONGODB_URL="mongodb://admin:qwerty@mongo:27017" `
  mongo-express

Docker compose
Docker compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services, networks, and volumes. Then, with a single command, you create and start all the services from your configuration.  
.yaml -> yet Another Markup Language

docker compose -f filName.yaml up -d
// to start the containers in detached mode, allowing them to run in the background.

docker compose -f filName.yaml down
// to delete all the containers, networks, and volumes defined in the Compose file.

Dockerizing our App
test app
   |
docker image
   |
container

Dockerfile instructions
https://docs.docker.com/get-started/docker-concepts/building-images/writing-a-dockerfile/

Their can be multiple run command but onlu one cmd command

Push image to docker hub