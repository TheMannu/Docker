# Docker and Docker Compose

Docker is a set of platform as a service products that use OS-level virtualization to deliver software in packages called containers. The service has both free and premium tiers.


## Getting Started:
- Docker Overview
- Docker Installation
- Docker Compose Installation
- Docker Volumes
- Docker Networking

## Certification:
- [Containers Fundamentals Certification](https://training.linuxfoundation.org/training/containers-fundamentals/)

## Docker and Docker Compose Tasks:

### 1. Install Docker and Docker Compose on Linux:

**Steps:**

- Update package list:
  ```bash
  sudo apt update
  ```

- Install dependencies:
  ```bash
  sudo apt update
  ```

- Add Docker's GPG key:
  ```bash
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  ```

- Add Docker repository:
  ```bash
  sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
  ```

- Update package list again:
  ```bash
  sudo apt update
  ```

- Install Docker Engine:
  ```bash
  sudo apt install -y docker-ce
  ```

- Verify Docker installation:
  ```bash
  sudo systemctl status docker
  ```

- Add user to Docker group:
  ```bash
  sudo usermod -aG docker $USER
  ```

- Download Docker Compose:
  ```bash
  sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  ```

- Set executable permissions for Docker Compose:
  ```bash
  sudo chmod +x /usr/local/bin/docker-compose
  ```

- Verify Docker Compose installation:
  ```bash
  docker-compose --version
  ```

### 2. Use Docker CLI to run an Nginx server locally and expose it on port 8080:
- Pull Nginx Image:
  ```bash
  sudo docker pull nginx
  ```

- Run Nginx Container:
  ```bash
  docker run -d -p 8080:80 --name my-nginx nginx
  ```

- Verify Nginx Container Status:
  ```bash
  docker ps
  ```

### 3. Docker Push an Image to Docker Hub:
```bash
docker tag my-image:latest myusername/my-image:latest
docker login
docker push myusername/my-image:latest
```

### 4. Run Docker Commands Without Sudo:
```bash
cat /etc/group | grep docker
sudo usermod -aG docker <username>
logout
groups
docker info
```

### 5. Learn Basic Docker CLI Commands:
```bash
# Display Docker version information
docker version

# Show detailed Docker system information
docker info

# List all Docker images
docker images

# List running containers
docker ps

# Pull a Docker image from a registry (e.g., Docker Hub)
docker pull <image-name>

# Create and start a new container based on an image
docker run <image-name>

# Create and start a container in detached mode (background)
docker run -d <image-name>

# Stop a running container
docker stop <container-id>

# Start a stopped container
docker start <container-id>

# Restart a container
docker restart <container-id>

# Remove a stopped container
docker rm <container-id>

# Remove a Docker image
docker rmi <image-id>

# Execute a command inside a running container in interactive mode
docker exec -it <container-id> <command>

# Display logs of a running container
docker logs <container-id>

# Build a Docker image from a Dockerfile and tag it
docker build -t <image-name> <path-to-dockerfile>

# Start services defined in a Docker Compose file
docker-compose up

# Stop and remove services defined in a Docker Compose file
docker-compose down
```

### 6. Write a Dockerfile to Create a Custom Nginx Server that Outputs "Hello World":
- Create Project Directory and Navigate:
  ```bash
  mkdir custom-nginx
  cd custom-nginx
  ```

- Create Dockerfile:
  ```bash
  cat > Dockerfile <<EOF
  FROM nginx:latest
  COPY nginx.conf /etc/nginx/nginx.conf
  RUN mkdir -p /usr/share/nginx/html
  COPY index.html /usr/share/nginx/html/index.html
  EXPOSE 80
  CMD ["nginx", "-g", "daemon off;"]
  EOF
  ```

- Create `nginx.conf`:
  ```bash
  cat > nginx.conf <<EOF
  worker_processes 1;
  events {
      worker_connections 1024;
  }
  http {
      server {
          listen 80;
          server_name localhost;
          location / {
              root /usr/share/nginx/html;
              index index.html;
          }
      }
  }
  EOF
  ```

- Create `index.html`:
  ```bash
  cat > index.html <<EOF
  <!DOCTYPE html>
  <html>
  <head>
      <title>Hello, World!</title>
  </head>
  <body>
      <h1>Hello, World!</h1>
  </body>
  </html>
  EOF
  ```

- Build Docker Image:
  ```bash
  docker build -t custom-nginx .
  ```

- Run Docker Container:
  ```bash
  docker run -p 8080:80 custom-nginx
  ```

### 7. Create a Docker Compose File with 3 Nginx Services Outputting "Hello World 1", "Hello World 2", and "Hello World 3":
- Create `docker-compose.yml`:
```bash
  cat > docker-compose.yml <<EOF
  version: '3.8'

  services:
    nginx1:
      image: nginx:latest
      ports:
        - "8081:80"
      environment:
        - MESSAGE=hello-world 1
      networks:
        - my-network

    nginx2:
      image: nginx:latest
      ports:
        - "8082:80"
      environment:
        - MESSAGE=hello-world 2
      networks:
        - my-network

    nginx3:
      image: nginx:latest
      ports:
        - "8083:80"
      environment:
        - MESSAGE=hello-world 3
      networks:
        - my-network

  networks:
    my-network:
  EOF

```

### 8. Attach Docker Volume and Read the File Dynamically in the Container from Outside:
(Details to be filled as per setup requirements)
