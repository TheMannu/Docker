
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