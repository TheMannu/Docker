
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
