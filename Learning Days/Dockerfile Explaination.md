
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

### Dockerfile, Keywords can be used to customized Images

#### **FROM**
- *Usage*:
    ```dockerfile
    FROM <image>
    FROM <image>:<tag>
    FROM <image>@<digest>
    ```

- *Information*:
    - `FROM` Must be the first non-comment instruction in the Dockerfile.
    - `FROM` can appear multiple times within a single Dockerfile to create multiple images.Simply make a note of the last image ID output by the commit before each new `FROM` command.
    - The `tag` or `digest` values are optional. If you omit either of them, the builder assumes `latest` by default.The builder returns an error if it cannot match the `tag` value.

#### **MAINTAINER**
- *Usage*:
    ```dockerfile
    MAINTAINER <name>
    ```
- Information:- Specifies the author of the image. Deprecated in favor of `LABEL`.

#### **RUN**
- *Usage*:
    ```dockerfile
    RUN <command> # (shell form, the command is run in a shell, which by default is /bin/sh -c on Linux or cmd/S/C on Windows)
    RUN ["<executable>", "<param1>", "<param2>"]  # (Exec form)
    ```
- *Information*:
    - The exec form is preferred to avoid shell munging. And to RUN commands using a base image that does not contain the specified shell executable.
    - For the shell form, `/bin/sh -c` is the default shell on Linux.
    - Normal shell processing does not occur when using the exec form. For example, `RUN ["echo", "$HOME"]` will not do variable substitution on `$HOME`.

#### **CMD**
- *Usage*:
    ```dockerfile
    CMD ["<executable>", "<param1>", "<param2>"]  # (exec form, this is the preferred form)
    CMD ["<param1>", "<param2>"]  # (as default parameters to ENTRYPOINT)
    CMD <command> <param1> <param2>  # (Shell form)
    ```
- *Information*:
    - Provides default arguments for a container.The main purpose of a `CMD` is to provide defaults for an executing container. These defaults can include an executable, or they can omit the executable, in which case you must specify an `ENTRYPOINT` instruction as well.

    - There can only be one `CMD` instruction in a Dockerfile. If you list more than one `CMD` then only the last `CMD` will take effect.

    - If `CMD` is used to provide default arguments for the `ENTRYPOINT` instruction, both the `CMD` and `ENTRYPOINT` instructions should be specified with the `JSON` array format.

    - If the user specifies arguments to docker run then they will override the default specified in `CMD`.

    - Normal shell processing does not occur when using the exec form. For example, `CMD ["echo", "$HOME"]` will not do variable substitution on `$HOME`.
