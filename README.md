This project cover following Docker concepts:

1. Production-Grade Workflow
2. Docker Volumes

# Docker

We can have multiple Dockerfile each for different environment like:

1. **Dockerfile.dev** => use this for local development server
2. **Dockerfile** => use this for production server

## To build docker custom image using specific file
```
docker build -f <file_name> -t <docker_hub_ID>/<custom_image_name> .

docker build -f Dockerfile.dev -t ishahroz/simple-dockerized-node-app .
```
## To run docker container including bookmarking and docker volume

**Docker Volume** essentially means to pass reference of files outside the container to the container. So, whenever there's change in those files, Docker client will automatically know and the changes will be reflected inside the container. In other words, we are not taking snapshot of file-system but instead passing reference to Docker.

**Bookmarking** means for some files we don't want Docker to use references but instead create their own files (like node_modules) or just take a snapshot of file-system outside the container.

```
docker run -p <local_port>:<container_port> -v /app/node_modules -v $(pwd):/app  <container_id>

docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app  ishahroz/simple-dockerized-node-app
```

In the above command, to exclude any folder or directory from being referenced via volume, we don't put colon (:) just like we didn't before "**-v /app/node_modeules**".
But to reference any folder or directory, we have to put colon (:) just like we did before "**$(pwd):/app**".

# docker-compose

## To run container using docker-compose including bookmarking and docker volume

We don't need to add the long command as above but instead create a "**docker-compose.yml**" file and define all the configurations in that file.

```
docker-compose up
```

Also, notice the following configuration:

```
build:
      context: .
      dockerfile: Dockerfile.dev
```

"**context**" means where the Dockerfile will be located in my project directory.
<br/>
"**dockerfile**" as it is obvious just means which Dockerfile to use.

