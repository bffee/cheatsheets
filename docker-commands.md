## Basic Docker Commands

```
docker pull <img-name>:<version>
```
```
docker pull nginx:1.23
```

downloads the perticular image from docker registery (Docker HUB)

```
docker images
```

to see all the downloaded images

```
docker run <image-name>:<tag>
```
```
docker run nginx:latest
```

to run the downloaded image


```
docker ps
```

to see all the running containers


```
docker logs <container-id>
```
```
docker logs d59cc16889a4
```

to see the logs of the containers

```
docker stop <container-id>
```
```
docker stop d59cc16889a4
```

to stop the running container

```
docker start <container-id>
```
```
docker start d59cc16889a4
```

to start the existing container

```
docker exec -it <container-id> sh
```
```
docker exec -it d59cc16889a4 sh
```

to start the container with the interactive shell inside

```
docker rm <container-id>
```
```
docker rm d59cc16889a4
```
to remove the stopped container

### Important Flags

- `-a` to see all the available containers

- `-d` - for running container in background

- `-p` - for binding the container port with machine port

- `-it` - to start a container in interactive mode

- `--name` - for giving name to the contianer

---

## Creating Dockerfile

1. creat a file `Dockerfile` in your project's root directory.

2. select a base image on which you want your application to run on.

3. copy all your application's source code into the container.

4. change your working directory into the source code folder inside the docker

5. run your application.

> you need to do this inside the Dockerfile using directives.

```
FROM <image-name>:<version>

COPY * /app/

WORKDIR /app

CMD [<command>, arguments]
```

```
FROM node

COPY * /app/

WORKDIR /app

CMD ["node", "server.js"]
```

### Docker Directives

`FROM` - directive is used to specify base image.

`COPY` - directive is used to copy files from your main system to container.

`WORKDIR` - directive is used to change your current working directory inside an container.

`CMD` - directive is used to run the shell commands inside an container.

---
## Creating Dcoker Image

```
docker build -t <img-name>:<tag> <dockerfile-path>
```

```
docker build -t my-app:1.0 .
```

to build a docker image from **Dockerfile**