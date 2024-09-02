
# Docker Installation and Usage Guide

## Install Docker

```bash
sudo -i
curl -fsSL https://get.docker.com -o install-docker.sh
ls
sudo sh install-docker.sh
```

## Verify Docker Installation

```bash
docker pull hello-world
docker images
docker run hello-world
docker ps    # Running processes
docker ps -a # All or archives
```

### Docker Initialization Steps

1. **The Docker client** contacted the Docker daemon.
2. **The Docker daemon** pulled the "hello-world" image from Docker Hub.
3. **The Docker daemon** created a new container from that image which runs the executable that produces the output you are currently reading.
4. **The Docker daemon** streamed that output to the Docker client, which sent it to your terminal.

## Docker Commands

### `docker pull` vs `docker run`

- `docker pull`: Download the image to your system.
- `docker run`: Download the image and create a container.

```bash
docker run -it ubuntu  # -it is interactive mode and moves inside the container at the beginning
exit

docker ps -a
docker start CONTAINER_ID
docker logs CONTAINER_ID
docker inspect CONTAINER_ID
docker rm CONTAINER_ID
docker exec -it CONTAINER_ID bin/bash  # Move inside the container anytime after starting
docker stop CONTAINER_ID
```

### Image and Container Sizes

- Ubuntu image: 78 MB
- Ubuntu operating system: 2 GB executable file, 6 GB runtime
- Smallest size of the Operating System Image: Alpine

### Container Lifecycle Commands

- `docker pause <container ID>`: Suspends all processes in the specified container.
- `docker stop <container ID>`: Kills the main process inside the container.
- `docker kill <container ID>`: Kills the container.
- `docker rm -f <container ID>`: Removes the container.
- `docker rmi -f <image name>`: Removes the image itself.
- `docker start <container ID>`

### Nginx Example

```bash
docker run nginx  # The nginx is working fine but not reachable from browser.
docker run -p 80:80 nginx  # Configure port 80 of nginx to port 80 of the machine.
docker run --name docker-nginx -p 80:80 nginx  # Assign a name to the container.
```

#### Serving Custom HTML with Nginx

```bash
mkdir -p ~/docker-nginx/html
cd ~/docker-nginx/html
vi index.html
```

```html
<html>
  <head>
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css" rel="stylesheet" integrity="sha256-MfvZlkHCEqatNoGiOXveE8FIwMzZg4W85qfrfIFBfYc= sha512-dTfge/zgoMYpP7QbHy4gWMEGsbsdZeCXz7irItjcC3sPUFtf0kuFbDz/ixG7ArTxmDjLXDmezHubeNikyKGVyQ==" crossorigin="anonymous">
    <title>Docker nginx Tutorial</title>
  </head>
  <body>
    <div class="container">
      <h1>Hello Learning team with Devanshau, Debyan, Sabir, Nisha</h1>
      <p>This nginx page is brought to you by Docker in front of Sri Ram, Arun, Ravi, Naveen, Sabita</p>
    </div>
  </body>
</html>
```

```bash
docker run --name docker-nginx -p 80:80 -d -v ~/docker-nginx/html:/usr/share/nginx/html nginx
```

## Jenkins Installation

```bash
docker run -it -d -p 8080:8080 jenkins/jenkins:latest
```

## Creating a Custom Docker Image

```dockerfile
# Dockerfile
FROM ubuntu
MAINTAINER clouddevopshub@gmail.com
RUN apt-get update                # OS level command
RUN apt-get install nginx -y      # OS level command
CMD ["echo", "Image created"]     # Application level command
```

### Build and Push Image

```bash
docker build -t mynginxbatch35 .  # Create image in the current directory with tag name mynginxbatch35
docker login
docker push themannu/mynginxbatch35
docker pull themannu/mynginxbatch35  # Verify the image is on Docker Hub
```

### Useful Resources

- [Dockerfile Blog](https://www.clouddevopshub.com/blog/dockerfile)
- [Dockerfile Examples](https://github.com/komljen/dockerfile-examples)

### Creating a Backup of an Image

1. Run the container:
   ```bash
   docker run -d -p 80:80 nginx
   ```
2. Commit the container to an image:
   ```bash
   docker commit CONTAINER_ID <new_image_name>
   ```
3. Take a backup of the image:
   ```bash
   docker save CONTAINER_NAME > mybackup.tar
   ls
   aws s3 cp mybackup.tar s3://your-bucket-name
   ```

### Docker Troubleshooting and Monitoring

```bash
docker inspect <container_name>
docker inspect <container_id>
docker logs <container_name>
docker logs <container_id>
docker logs -f <container_name>  # Real-time log
docker stats <container_id>
docker top <container_name>
docker top <container_id>
```

### Cleanup or Prune Unused (Dangling) Images

```bash
docker system df
docker image prune -a
```
