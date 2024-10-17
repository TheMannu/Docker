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