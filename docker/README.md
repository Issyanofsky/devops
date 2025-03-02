

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

## Data Volume

  docker run -p 80:80 -v /var/www

  docker volume ls - display volumes list.

  (docker run -p 80:80 -v $(PWD):/var/www <image_name>) - run the container (image), connect ports 80 to 80, mount local(PWD) to /var/www in container.

  (docker run --name <container_name> -p 80:80 -v c:\users:/user/shared/nginx/html:ro -d nginx) - deploy nginx, connect ports 80 tp 80, run in background (-d), mount a read-only (ro) drive located localy on c:users mounted on /user/shared/nginx/html).

  (docker run --name <container_name> -v source_location:des_location -e MYSQL_ROOT_PASSWORD=a1a1a1 -d mysql) - run container in the background (-d), mount a drive and pass a env variable (password).

# Key Dockerfile Instactions

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
  
    
  


  
