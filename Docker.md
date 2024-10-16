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