## Download and install Docker.

---

### **Scripting Approach to Download and Install Docker**

1. **Switch to root user**:
```bash
   sudo -i  # Change to root user for installation permissions
```

2. **Download Docker installation script**:
```bash
   curl -fsSL https://get.docker.com -o install-docker.sh  # Download the Docker installation script
```

3. **List files to verify the script is downloaded**:
```bash
   ls  # List files in the current directory to confirm the script's presence
```

4. **Run the installation script**:
```bash
   sudo sh install-docker.sh  # Execute the Docker installation script
```

---


### **Verify Docker Installation**

1. **Pull the `hello-world` image**:
```bash
   docker pull hello-world  # Download the 'hello-world' image from Docker Hub
```

2. **List downloaded Docker images**:
```bash
   docker images  # Display all Docker images present on the system
```

3. **Run the `hello-world` container**:
```bash
   docker run hello-world  # Create and run a container from the 'hello-world' image
```

4. **List running containers**:
```bash
   docker ps  # Show currently running Docker containers
```

5. **List all containers (including stopped ones)**:
```bash
   docker ps -a  # Display all containers, including those that are stopped
```

---

### **To generate this message, Docker took the following steps:**

1. The Docker client contacted the Docker daemon.
2. The Docker daemon pulled the "hello-world" image from the Docker Hub (amd64).
3. The Docker daemon created a new container from that image, which runs the executable that produces the output you are currently reading.
4. The Docker daemon streamed that output to the Docker client, which sent it to your terminal.

---

### **Docker `pull` vs. Docker `run`**

- **`docker pull`**: Downloads the image to your system.
- **`docker run`**: Downloads the image (if not present) and creates a container to run the image.

---

### **Container Management Commands**

1. **Run Ubuntu in interactive mode**:
```bash
   docker run -it ubuntu  # Start an interactive Ubuntu container
```

2. **Exit the container**:
```bash
   exit  # Exit from the running container's shell
```

3. **List all containers again**:
```bash
   docker ps -a  # Show all containers to check the state of the previously started container
```

4. **Start a stopped container**:
```bash
   docker start <CONTAINER ID>  # Start a container that is stopped
```

5. **View container logs**:
```bash
   docker logs <CONTAINER ID>  # Retrieve logs from a specified container
```

6. **Inspect container details**:
```bash
   docker inspect <CONTAINER ID>  # Display detailed information about a container
```

7. **Remove a container**:
```bash
   docker rm <CONTAINER ID>  # Delete a specified container
```

8. **Execute a command inside a running container**:
```bash
   docker exec -it <CONTAINER ID> bin/bash  # Run a bash shell inside a running container
```

9. **Stop a running container**:
```bash
   docker stop <CONTAINER ID>  # Stop a running container gracefully
```

---

### **Image and OS Size Comparison**

- **Ubuntu Docker Image**: 78MB  
- **Ubuntu Full Operating System**: 2GB executable file, 6GB when running.

---

### **Smallest OS Image**:  
- **Alpine Linux** is the smallest Docker image.

---
### **Container Lifecycle Commands**

1. **Pause all processes in a container**:
```bash
   docker pause <CONTAINER ID>  # Suspend all processes in the specified container
```

2. **Stop the main process in a container**:
```bash
   docker stop <CONTAINER ID>  # Gracefully stop the main process in a specified container
```

3. **Forcefully kill a container**:
 ```bash
   docker kill <CONTAINER ID>  # Immediately kill a running container
```

4. **Forcefully remove a container**:
```bash
   docker rm -f <CONTAINER ID>  # Forcefully delete a specified container
```

5. **Forcefully remove an image**:
```bash
   docker rmi -f <image name>  # Forcefully delete a specified Docker image
```

6. **Start a stopped container**:
```bash
   docker start <CONTAINER ID>  # Restart a previously stopped container
```

---

### **Working with Nginx**

1. **Run Nginx (unreachable by browser)**:
```bash
   docker run nginx  # Start an Nginx container without port mapping
```

2. **Run Nginx with port configuration**:
```bash
   docker run -p 80:80 nginx  # Map port 80 of the container to port 80 of the host
```

3. **Run Nginx with a custom container name**:
```bash
   docker run --name docker-nginx -p 80:80 nginx  # Start Nginx container with a specified name
```

---

### **Serving Custom HTML with Nginx**

1. **Create a directory for HTML files**:
```bash
   mkdir -p ~/docker-nginx/html  # Create a directory for Nginx HTML files
   cd ~/docker-nginx/html  # Navigate to the HTML directory
   vi index.html  # Create or edit an index.html file for the Nginx server
```

2. **Run Nginx with a mounted volume for HTML**:
```bash
   docker run --name docker-nginx -p 80:80 -d -v ~/docker-nginx/html:/usr/share/nginx/html nginx  # Run Nginx with a volume for custom HTML
```

---

### **Custom HTML Content**
```html
<html>
  <head>
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css" rel="stylesheet" integrity="sha256-MfvZlkHCEqatNoGiOXveE8FIwMzZg4W85qfrfIFBfYc= sha512-dTfge/zgoMYpP7QbHy4gWMEGsbsdZeCXz7irItjcC3sPUFtf0kuFbDz/ixG7ArTxmDjLXDmezHubeNikyKGVyQ==" crossorigin="anonymous">
    <title>Docker nginx Tutorial</title>
  </head>
  <body>
    <div class="container">
      <h1>Hello Learning team with Devanshau, Debyan, Sabir, Nisha</h1>
      <p>This nginx page is brought to you by Docker, in front of Sri Ram, Arun, Ravi, Naveen, Sabita</p>
    </div>
  </body>
</html>
```

---