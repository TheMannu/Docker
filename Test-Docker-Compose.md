# Project-Docker-Compose

You and your team have to build a web application based on **nginx** in three supported versions:

- **mainline**: Uses nginx version `1.17.9-perl`
- **stable**: Uses a version defined in the `.env` file (variable `DEFAULT_NGINX_VERSION`)
- **alpine**: Uses nginx version `1.17.9-alpine-perl`

Your role is to create a **single `docker-compose.yaml`** file with configuration for the three services, named exactly as the versions listed above.

All services should be built using **nginx.Dockerfile** with the following content (located in the same directory as the `docker-compose.yaml` file):
