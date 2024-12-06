# Project-Docker-Compose

You and your team have to build a web application based on **nginx** in three supported versions:

- **mainline**: Uses nginx version `1.17.9-perl`
- **stable**: Uses a version defined in the `.env` file (variable `DEFAULT_NGINX_VERSION`)
- **alpine**: Uses nginx version `1.17.9-alpine-perl`

Your role is to create a **single `docker-compose.yaml`** file with configuration for the three services, named exactly as the versions listed above.

All services should be built using **nginx.Dockerfile** with the following content (located in the same directory as the `docker-compose.yaml` file):

```
ARG NGINX_VERSION
ARG BUILD_FILE
FROM nginx:${NGINX_VERSION}
COPY ${BUILD_FILE} /etc/nginx/conf.d
```

## Requirements:
- **All images** should be built as `app` with the supported version as a tag.
- The **stable** service should use a version value tag from the variable `DEFAULT_NGINX_VERSION` in the `.env` file.
- The **mainline** and **stable** services should use `debian.conf` as the `BUILD_FILE` argument.
- The **alpine** service should use `alpine.conf` as the `BUILD_FILE` argument.
  
Both `debian.conf` and `alpine.conf` are located in the same directory as `docker-compose.yaml`.


## Example Directory Structure:
```shell
test-solver@codility:/task/docker_compose_build$ ls -al app
total 12
drwxrwxr-x 3 test-solver test-solver 4096 Mar  7 13:58 .
drwxrwxr-x 6 test-solver test-solver 4096 Mar  7 13:57 ..
-rw-rw-r-- 1 test-solver test-solver 4096 Mar  7 13:58 alpine.conf
-rw-rw-r-- 1 test-solver test-solver 4096 Mar  7 13:58 debian.conf
-rw-rw-r-- 1 test-solver test-solver 4096 Mar  7 13:57 docker-compose.yaml
drwxrwxr-x 7 test-solver test-solver 4096 Mar  7 13:57 .git
-rw-rw-r-- 1 test-solver test-solver 4096 Mar  7 13:57 nginx.Dockerfile
-rw-rw-r-- 1 test-solver test-solver 4096 Mar  7 13:57 .env
```

### Docker Compose Configuration:

1. Define three services: `mainline`, `stable`, and `alpine`.
2. Ensure each service uses the correct **nginx** version and **BUILD_FILE**.
3. Execute the build process in the `app` directory as outlined above.

### Docker Compose Setup for NGINX Application

To build and configure the web application using NGINX in three supported versions (`mainline`, `stable`, and `alpine`), you need to create a `docker-compose.yaml` file that defines services for each version and builds them from the same `nginx.Dockerfile`. Below is a step-by-step guide to implementing the solution based on the provided specifications.

### Steps:

1. **Create `.env` File**
   - This file should contain the default NGINX version to be used for the `stable` service.
   - Add the following line to `.env`:
     ```bash
     DEFAULT_NGINX_VERSION=1.18.0
     ```

2. **Create `nginx.Dockerfile`**
   - The `Dockerfile` will handle the build process for each version of NGINX. It should look like this:
     ```Dockerfile
     ARG NGINX_VERSION
     ARG BUILD_FILE
     FROM nginx:${NGINX_VERSION}
     COPY ${BUILD_FILE} /etc/nginx/conf.d/default.conf
     ```


3. **Create the `docker-compose.yaml` File**
   - In the same directory as `nginx.Dockerfile`, create the `docker-compose.yaml` with the following content:
   
     ```yaml
     version: '3.7'
     services:
       mainline:
         build:
           context: .
           dockerfile: nginx.Dockerfile
           args:
             NGINX_VERSION: 1.17.9-perl
             BUILD_FILE: debian.conf
         image: app:1.17.9-perl

       stable:
         build:
           context: .
           dockerfile: nginx.Dockerfile
           args:
             NGINX_VERSION: ${DEFAULT_NGINX_VERSION}
             BUILD_FILE: debian.conf
         image: app:${DEFAULT_NGINX_VERSION}

       alpine:
         build:
           context: .
           dockerfile: nginx.Dockerfile
           args:
             NGINX_VERSION: 1.17.9-alpine-perl
             BUILD_FILE: alpine.conf
         image: app:1.17.9-alpine-perl
     ```

4. **Build Arguments**
   - Each service builds from `nginx.Dockerfile` using the `NGINX_VERSION` and `BUILD_FILE` as arguments.
   - The `mainline` and `stable` services use `debian.conf`, while the `alpine` service uses `alpine.conf`.

5. **Running the Build**
   - Navigate to the directory containing `docker-compose.yaml` and run:
     ```bash
     docker-compose up --build
     ```


### Directory Structure

Ensure the following files are in place:

- `docker-compose.yaml`
- `nginx.Dockerfile`
- `debian.conf`
- `alpine.conf`
- `.env` (with `DEFAULT_NGINX_VERSION` variable)
