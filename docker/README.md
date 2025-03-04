<div align="center">

# **Docker**

</div>


## docker info

  check if installed - retrive info on docker.

## docker images

  display list of docker images.

## docker pull

  docker pull <image_name>:<tag> - pull image from dockerHub.

## docker run

  docker run <image_name>:<tag> - run an image in a container.

## docker ps

    (docker ps) - list running containers

    (docker ps -a) - display all containers (including stoped).

## docker rm

  docker rm <container _name> - delete docker container.

## docker rmi

  docker rmi <image_name> - delete docker image.

## docker exec

  execute command into a container

  docker exec -it <container_name> <command>

  (docker exec -it <container_name> /bin/bash) - open bash prompt in the container.

## docker stop

  docker stop  <container_name>  - stop container 

## docker inspect

  docker inspect <image_name> - inspect the image logs

## docker logs 

  retrieve the logs of a running or stopped container.

  docker logs [OPTIONS] CONTAINER_NAME_OR_ID

  (docker logs -t my_container) - Includes timestamps in the log output.

## Data Volume

  docker run -p 80:80 -v /var/www

  docker volume ls - display volumes list.

  (docker run -p 80:80 -v $(PWD):/var/www <image_name>) - run the container (image), connect ports 80 to 80, mount local(PWD) to /var/www in container.

  (docker run --name <container_name> -p 80:80 -v c:\users:/user/shared/nginx/html:ro -d nginx) - deploy nginx, connect ports 80 tp 80, run in background (-d), mount a read-only (ro) drive located localy on c:users mounted on /user/shared/nginx/html).

  (docker run --name <container_name> -v source_location:des_location -e MYSQL_ROOT_PASSWORD=a1a1a1 -d mysql) - run container in the background (-d), mount a drive and pass a env variable (password).

## docker stats

  docker stats - display real-time statistics about the resource usage (CPU, memory, disk I/O, network I/O, etc.) of running containers. 

  docker stats [OPTIONS] [CONTAINER...]

  (docker stats my_container_name) - show stats for a specific container.

  (docker stats) - show stats for all containers.

## docker Top

  docker top - display the running processes inside a Docker container.

  docker top <container_name_or_id>

<div align="center">

# **Docker Install**

</div>
    install package:
    
      sudo apt update

    install Docker:

      sudo apt install docker-ce

  Start and enable Docker service:

      sudo systemctl start docker

      sudo systemctl enable docker
      
  Verify Docker installation:

      sudo docker --version
  
  Run Docker without sudo:

      sudo usermod -aG docker $USER
    
  
# Key Dockerfile Instactions

  by default the docker file caled Dockefile.
  
  ## FROM

    FROM - Specifies the base image to use for the Docker image.

    (FROM ubuntu:20.04)
  
  ## MAINTAINER

    MAINTAINER - Defines the author of the Dockerfile.

  ## RUN

    RUN - Executes a command during the build process of the image. This could be installing packages, or setting up files.

    (RUN apt-get update && apt-get install -y curl)

  ## COPY

    COPY - Copies files or directories from the host machine to the container's filesystem.

    (COPY ./myapp /app)

  ## ENTRYPOINT

    ENTRYPOINT - Defines the main command to run when the container starts. It is used to set a default command that can’t be overridden unless CMD is used.

    (ENTRYPOINT ["python", "app.py"])

  ## WORKDIR

    WORKDIR - Sets the working directory for any following RUN, CMD, ENTRYPOINT, COPY, or ADD instructions.

    (WORKDIR /app)

  ## EXPOSE

    EXPOSE - Informs Docker that the container listens on the specified network ports at runtime.

    (EXPOSE 8080)
    
  ## ENV

    ENV - Sets an environment variable in the container.

    (ENV APP_ENV=production)

  ## VOLUME

    VOLUME - Creates a mount point and attaches it to a container, typically for persistent data storage.

    (VOLUME ["/data"])

## ARG

  ARG - Defines a build-time variable that can be passed to the Docker build command.

  (ARG VERSION=1.0) - defines a build-time argument VERSION with a default value of 1.0.

## CMD

  CMD - Specifies the default command to run when the container starts.

  (CMD ["python", "app.py"]) -  default command that gets run when the container starts, unless overridden by the user.
  



# build

  ## docker build 

    docker build . - (from the directory with the Dockerfile) - builds the image

    (docker build . -t <image_name>) - build a image with a name describe.

# DockerHub

  ## docker tag 

    docker tag <source_image>:<tag> <destinain_image_name>:<tag> - change image name.

  ## docker login

    docker login - log to DockerHub.

  ## docker push

    docker push <image_name>:<tag> - push an image to docker hub repository.


# Docker Network

## docker network ls

  display networks list.

## docke network inspect

  docker network inspect <network_name> - info about the network.

## docker netwrok create

  create a network in docker.

  docker network create [OPTIONS] NETWORK_NAME

  options:

    --driver bridge (none-closeNetwork, host-only inside containers, bridge-overlay network(open to all)).
    --subnet 192.168.1.0/24
    --gateway 192.168.1.1
    --internal - Creates an internal network where containers can only communicate with each other, not with the external network.
    --label "env=production"

## docker network connect
  
  connect a running container to an existing Docker network.

  docker network connect [OPTIONS] NETWORK_NAME CONTAINER_NAME_OR_ID

## docker network disconnect

  disconnect a running container from a network.

  docker network disconnect [OPTIONS] NETWORK_NAME CONTAINER_NAME_OR_ID



# Docker Compose

   define and manage multi-container Docker applications.  writen in YAML.


      version: '3'  # Version of the docker-compose file format
          services:     # Defines the services (containers)
          web:
            image: nginx:latest     # The web service uses the official Nginx image
            ports:
              - "8080:80"           # Expose the container's port 80 on the host's port 8080
          db:
            image: postgres:latest  # The db service uses the official Postgres image
            environment:
              POSTGRES_PASSWORD: example_password  # Environment variable for database password

## docker-compose up

  Starts all the containers defined in the docker-compose.yml file

  (docker-compose up -d) - Starts the containers in detached mode, meaning they run in the background.

## docker-compose down

  docker-compose down - Stops and removes the containers, networks, and volumes created by docker-compose up.

  docker-compose down

## docker-compose logs

  docker-compose logs - Shows the logs from the containers started with Docker Compose.

  (docker-compose logs)

## docker-compose ps

  docker-compose ps - Lists the containers that are running as part of the Compose application.

  (docker-compose ps)

## docker-compose build

  docker-compose build -  build or rebuild services defined in a docker-compose.yml file.

  docker-compose build [OPTIONS] [SERVICE...]

  (docker-compose build web) - build a specific service (e.g., web).
 
 
  


  
