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
