# Coredns-docker 💀🐳 #


[![GitHub Build Status](https://github.com/xvxd4sh/coredns-docker/workflows/build/badge.svg)](https://github.com/xvxd4sh/coredns-docker/actions/workflows/build.yml)
[![CodeQL](https://github.com/xvxd4sh/coredns-docker/workflows/CodeQL/badge.svg)](https://github.com/xvxd4sh/coredns-docker/actions/workflows/codeql-analysis.yml)
[![Known Vulnerabilities](https://snyk.io/test/github/xvxd4sh/coredns-docker/badge.svg)](https://snyk.io/test/github/xvxd4sh/coredns-docker)

## Docker Image ##

[![Docker Pulls](https://img.shields.io/docker/pulls/xvxd4sh/coredns)](https://hub.docker.com/r/xvxd4sh/coredns)
[![Docker Image Size (latest by date)](https://img.shields.io/docker/image-size/xvxd4sh/coredns)](https://hub.docker.com/r/xvxd4sh/coredns)
[![Platforms](https://img.shields.io/badge/platforms-amd64%20%7C%20arm%2Fv6%20%7C%20arm%2Fv7%20%7C%20arm64%20%7C%20ppc64le%20%7C%20s390x-blue)](https://hub.docker.com/r/xvxd4sh/coredns-docker/tags)

This is a docker project that is used to spin up a CoreDNS server.

## Running ##

### Running with Docker ###

To run the `xvxd4sh/coredns` image via Docker:

```console
docker run xvxd4sh/coredns:latest
```

### Running with Docker Compose ###

1. Modify the `docker-compose.yml` file similar to the one below to use [Docker Compose](https://docs.docker.com/compose/).

    ```yaml
    ---
    version: "3.7"

    # This Docker composition file is used to build and test the container

    secrets:
      quote_txt:
        file: ./src/secrets/quote.txt

    services:
      redirect-dns:
        # Run the container normally
        build:
          # VERSION must be specified on the command line:
          # e.g., --build-arg VERSION=0.0.1
          context: .
          dockerfile: Dockerfile
        image: xvxd4sh/coredns:latest
        container_name: coredns
        init: true
        restart: on-failure
        volumes:
          - './config:/root'
    ```

1. Start the container and detach:

    ```console
    docker compose up --detach
    ```

<!-- ## Using secrets with your container ##

This container also supports passing sensitive values via [Docker
secrets](https://docs.docker.com/engine/swarm/secrets/).  Passing sensitive
values like your credentials can be more secure using secrets than using
environment variables.  See the
[secrets](#secrets) section below for a table of all supported secret files.

1. To use secrets, create a `quote.txt` file containing the values you want set:

    ```text
    Better lock it in your pocket.
    ```

1. Then add the secret to your `docker-compose.yml` file:

    ```yaml
    ---
    version: "3.7"

    secrets:
      quote_txt:
        file: quote.txt

    services:
      example:
        image: xvxd4sh/coredns:latest
        volumes:
          - type: bind
            source: <your_log_dir>
            target: /var/log
        environment:
          - ECHO_MESSAGE="Hello from docker compose"
        ports:
          - target: 8080
            published: 8080
            protocol: tcp
        secrets:
          - source: quote_txt
            target: quote.txt
    ``` -->

## Updating your container ##

### Docker Compose ###

1. Pull the new image from Docker Hub:

    ```console
    docker compose pull
    ```

1. Recreate the running container by following the [previous instructions](#running-with-docker-compose):

    ```console
    docker compose up --detach
    ```

### Docker ###

1. Stop the running container:

    ```console
    docker stop <container_id>
    ```

1. Pull the new image:

    ```console
    docker pull xvxd4sh/coredns:latest
    ```

1. Recreate and run the container by following the [previous instructions](#running-with-docker).

## Volumes ##

| Mount point | Purpose        |
|-------------|----------------|
| `./config:/root`  |  Specifies the addresses for redirection  |

## Ports ##

The following ports are exposed by this container:

| Port | Purpose        |
|------|----------------|
| 53 | This is listening for DNS queries |

The sample [Docker composition](docker-compose.yml) publishes the
exposed port at 53.

## Environment variables ##

### Required ###

There are no required environment variables.

<!--
| Name  | Purpose | Default |
|-------|---------|---------|
| `REQUIRED_VARIABLE` | Describe its purpose. | `null` |
-->

<!--
### Optional ###

 | Name  | Purpose | Default |
|-------|---------|---------|
| `ECHO_MESSAGE` | Sets the message echoed by this container.  | `Hello World from Dockerfile` | -->

<!--
## Secrets ##

| Filename     | Purpose |
|--------------|---------|
| `quote.txt` | Replaces the secret stored in the example library's package data. | -->

<!-- ## Building from source ##

Build the image locally using this git repository as the [build context](https://docs.docker.com/engine/reference/commandline/build/#git-repositories):

```console
docker build \
  --build-arg VERSION=0.0.1 \
  --tag cisagov/example:0.0.1 \
  https://github.com/cisagov/example.git#develop
``` -->

## Cross-platform builds ##

To create images that are compatible with other platforms, you can use the
[`buildx`](https://docs.docker.com/buildx/working-with-buildx/) feature of
Docker:

1. Copy the project to your machine using the `Code` button above
   or the command line:

    ```console
    git clone https://github.com/xvxd4sh/coredns-docker.git
    cd coredns-docker
    ```

1. Create the `Dockerfile-x` file with `buildx` platform support:

    ```console
    ./buildx-dockerfile.sh
    ```

1. Build the image using `buildx`:

    ```console
    docker buildx build \
      --file Dockerfile-x \
      --platform linux/amd64 \
      --build-arg VERSION=0.0.1 \
      --output type=docker \
      --tag xvxd4sh/coredns:latest .
    ```

<!-- ## New repositories from a skeleton ##

Please see our [Project Setup guide](https://github.com/cisagov/development-guide/tree/develop/project_setup)
for step-by-step instructions on how to start a new repository from
a skeleton. This will save you time and effort when configuring a
new repository! -->

<!-- ## Contributing ##

We welcome contributions!  Please see [`CONTRIBUTING.md`](CONTRIBUTING.md) for
details. -->

## License ##

This project is in the worldwide [public domain](LICENSE).

This project is in the public domain within the United States, and
copyright and related rights in the work worldwide are waived through
the [CC0 1.0 Universal public domain
dedication](https://creativecommons.org/publicdomain/zero/1.0/).

All contributions to this project will be released under the CC0
dedication. By submitting a pull request, you are agreeing to comply
with this waiver of copyright interest.
