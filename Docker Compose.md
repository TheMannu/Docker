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
