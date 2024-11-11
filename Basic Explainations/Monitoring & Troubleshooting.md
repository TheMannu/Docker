### **Docker Troubleshooting / Monitoring Commands**

1. **Inspect container details**:
   ```bash
   docker inspect <container name>  # Display detailed information about a specified container
   ```

2. **Inspect container by ID**:
   ```bash
   docker inspect <container id>  # Show detailed information about a specified container by its ID
   ```

3. **View container logs**:
   ```bash
   docker logs <container name>  # Retrieve logs from a specified container
   ```

4. **View logs by container ID**:
   ```bash
   docker logs <container id>  # Get logs from a specified container using its ID
   ```

5. **View real-time logs**:
   ```bash
   docker logs -f <container name>  # Stream real-time logs from a specified container
   ```

6. **View resource usage statistics**:
   ```bash
   docker stats <container ID>  # Display resource usage statistics for a specified container
   ```

7. **Show processes running in a container**:
   ```bash
   docker top <container name>  # Display the processes running inside a specified container
   ```

8. **Show processes by container ID**:
   ```bash
   docker top <container id>  # List processes running in a specified container using its ID
   ```

---