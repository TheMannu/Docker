
## Dockerfile Commands and Usage

### Example Dockerfile
```dockerfile
FROM golang:1.20-alpine
WORKDIR /src
COPY .
RUN go mod download
RUN go build -o /bin/client ./cmd/client
RUN go build -o /bin/server ./cmd/server
ENTRYPOINT ["/bin/server"]
```


### What is a Dockerfile?
A Dockerfile is a text document that contains all the commands needed to assemble an image. Docker can automatically build images by reading the instructions from the Dockerfile.

### Simple Dockerfile Example
```dockerfile
FROM ubuntu
MAINTAINER clouddevopshub@gmail.com
RUN apt-get update
RUN apt-get install nginx -y
CMD ["echo", "Image created"]
```

### Common Dockerfile Commands Overview

- **FROM**: Select the base image
- **RUN**: Execute specified command
- **ENTRYPOINT**: Specifies the command to run the container
- **CMD**: Specifies a command to run at the time of container execution (can be overridden)
- **COPY**: Simple copy of files/directories from host to container
- **ADD**: Similar to `COPY` but with additional features like downloading from URLs (not recommended)
- **ENV**: Set environment variables
- **EXPOSE**: Opens designated port
- **WORKDIR**: Changes the current directory
- **MAINTAINER**: Deprecated (use `LABEL` instead)
