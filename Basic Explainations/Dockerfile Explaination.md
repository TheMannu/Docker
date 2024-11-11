
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

#### **LABEL**
- *Usage*:
    ```dockerfile
    LABEL <key>=<value> [<key>=<value> ...]
    ```
- *Information*:
    - The `LABEL` instruction adds metadata to an image.
    - To include spaces within a `LABEL` value, use quotes and backslashes as you would in command-line parsing.
    - Labels are additive including `LABELS` in `FROM` images.
    - If Docker encounters a label/key that already exists, the new value overrides any previous labels with identical keys.
    - To view an image’s labels, use the `docker inspect` command. They will be under the `"Labels"` JSON attribute.

#### **EXPOSE**
- *Usage*:
    ```dockerfile
    EXPOSE <port> [<port> ...]
    ```
- *Information*:
    - Informs Docker that the container listens on the specified network port(s) at runtime. 
    - `EXPOSE` Does not make the ports accessible to the host.

#### **ENV**
- *Usage*:
    ```dockerfile
    ENV <key> <value>
    ENV <key>=<value> [<key>=<value> ...]
    ```
- *Information*:
    - The ENV instruction sets the environment variable <key> to the value <value>.
    - The value will be in the environment of all “descendant” Dockerfile commands and can be replaced inline as well.
    - The environment variables set using ENV will persist when a container is run from the resulting image.
    - The first form will set a single variable to a value with the entire string after the first space being treated as the <value> - including characters such as spaces and quotes.

#### **ADD**
- *Usage*:
    ```dockerfile
    ADD <src> [<src> ...] <dest> #(this form is required for paths containing whitespace)
    ```
- *Information*:
    - Copies new files, directories, or remote file URLs from <src> and adds them to the filesystem of the image at the path <dest>.
    - <src> may contain wildcards and matching will be done using Go’s filepath.Match rules.
    - If <src> is a file or directory, then they must be relative to the source directory that is being built (the context of the build).
    - <dest> is an absolute path, or a path relative to WORKDIR.
    - If <dest> doesn’t exist, it is created along with all missing directories in its path.

#### **COPY**
- *Usage*:
    ```dockerfile
    COPY <src> [<src> ...] <dest>
    COPY ["<src>", ... "<dest>"] #(this form is required for paths containing whitespace)
    ```
- *Information*:
    - Copies new files or directories from <src> and adds them to the filesystem of the image at the path <dest>.
    - <src> may contain wildcards and matching will be done using Go’s filepath.Match rules.
    - <src> must be relative to the source directory that is being built (the context of the build).
    - <dest> is an absolute path, or a path relative to WORKDIR.
    - If <dest> doesn’t exist, it is created along with all missing directories in its path.

#### **ENTRYPOINT**
- *Usage*:
    ```dockerfile
    ENTRYPOINT ["<executable>", "<param1>", "<param2>"]  # Exec form, prefered
    ENTRYPOINT <command> <param1> <param2>  # Shell form
    ```
- *Information*: 
    - Allows you to configure a container that will run as an executable.
    - Command line arguments to docker run <image> will be appended after all elements in an exec form ENTRYPOINT and will override all elements specified using CMD.
    - The shell form prevents any CMD or run command line arguments from being used, but the ENTRYPOINT will start via the shell. This means the executable will not be PID 1 nor will it receive UNIX signals. Prepend exec to get around this drawback.
    - Only the last ENTRYPOINT instruction in the Dockerfile will have an effect.

#### **VOLUME**
- *Usage*:
    ```dockerfile
    VOLUME ["<path>", ...]
    VOLUME <path> [<path> ...]
    ```
- *Information*:
    - Creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers.

#### **USER**
- *Usage*:
    ```dockerfile
    USER <username | UID>
    ```
- *Information*:
    - The `USER` instruction sets the user name or UID to use when running the image and for any `RUN`, `CMD` and `ENTRYPOINT` instructions that follow it in the Dockerfile.
    
    Reference - Best Practices

#### **WORKDIR**
- *Usage*:
    ```dockerfile
    WORKDIR </path/to/workdir>
    ```
- **Information**:
    - Sets the working directory for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, and `ADD` instructions that follow it.
    - It can be used multiple times in the one Dockerfile. If a relative path is provided, it will be relative to the path of the previous `WORKDIR` instruction.

#### **ARG**
- *Usage*:
    ```dockerfile
    ARG <name>[=<default value>]
    ```
- *Information*:
    - Defines a variable that users can pass at build-time to the builder with the docker build command using the `--build-arg <varname>=<value>` flag.
    - Multiple variables may be defined by specifying ARG multiple times.
    - It is not recommended to use build-time variables for passing secrets like github keys, user credentials, etc. Build-time variable values are visible to any user of the image with the docker history command.
    - Environment variables defined using the ENV instruction always override an ARG instruction of the same name.
    - Docker has a set of predefined ARG variables that you can use without a corresponding ARG instruction in the Dockerfile.
        - HTTP_PROXY and http_proxy
        - HTTPS_PROXY and https_proxy
        - FTP_PROXY and ftp_proxy
        - NO_PROXY and no_proxy

#### **ONBUILD**
- *Usage*:
    ```dockerfile
    ONBUILD <Dockerfile INSTRUCTION>
    ```
- *Information*:
    - Adds to the image a trigger instruction to be executed at a later time, when the image is used as the base for another build. The trigger will be executed in the context of the downstream build, as if it had been inserted immediately after the `FROM` instruction in the downstream Dockerfile.
    - Any build instruction can be registered as a trigger.
    - Triggers are inherited by the "child" build only. In other words, they are not inherited by "grand-children" builds.
    - The `ONBUILD` instruction may not trigger `FROM`, `MAINTAINER`, or `ONBUILD` instructions.
