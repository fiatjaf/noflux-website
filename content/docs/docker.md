---
title: Noflux Installation with Docker
description: Instructions to install Noflux with Docker
url: docs/docker.html
---

This document describes how to use the Docker images of Noflux.

- [Container Registries](#registries)
- [How to Run the Container Manually](#docker)
- [Docker Compose](#docker-compose)

<h2 id="registries">Container Registries <a class="anchor" href="#registries" title="Permalink">¶</a></h2>

**Docker Registries:**

Docker images are published to three different container registries:

- [Docker Hub Registry](https://hub.docker.com/r/noflux/noflux): `docker.io/noflux/noflux`
- [GitHub Container Registry](https://github.com/fiatjaf/noflux/pkgs/container/noflux): `ghcr.io/noflux/noflux`
- [Quay.io RedHat Container Registry](https://quay.io/repository/noflux/noflux): `quay.io/noflux/noflux`

**Docker Architectures:**

- `amd64`
- `arm64`
- `arm/v7`
- `arm/v6`

**Docker Tags Naming Convention:**

- `latest`: Latest stable version
- `2.0.25`: Specific version
- `nightly`: Development version

The recommendation is to use a pinned version to avoid unexpected updates.

<h2 id="docker">How to Run the Container Manually <a class="anchor" href="#docker" title="Permalink">¶</a></h2>

Pull the image and run the container:

```bash
docker run -d \
  -p 80:8080 \
  --name noflux \
  -e "DATABASE_URL=postgres://noflux:*password*@*dbhost*/noflux?sslmode=disable" \
  -e "RUN_MIGRATIONS=1" \
  -e "CREATE_ADMIN=1" \
  -e "ADMIN_USERNAME=*username*" \
  -e "ADMIN_PASSWORD=*password*" \
  docker.io/noflux/noflux:latest
```

Running the command above will run the migrations and sets up a new admin account with the chosen username and password.

Once the container is started, you should be able to access the application on the exposed port which is port 80 in this example.

<h2 id="docker-compose">Docker Compose <a class="anchor" href="#docker-compose" title="Permalink">¶</a></h2>

Here is an example of a Docker Compose file:

```yaml
services:
  noflux:
    image: noflux/noflux:latest
    ports:
      - "80:8080"
    depends_on:
      db:
        condition: service_healthy
    environment:
      - DATABASE_URL=postgres://noflux:secret@db/noflux?sslmode=disable
      - RUN_MIGRATIONS=1
      - CREATE_ADMIN=1
      - ADMIN_USERNAME=admin
      - ADMIN_PASSWORD=test123
  db:
    image: postgres:17-alpine
    environment:
      - POSTGRES_USER=noflux
      - POSTGRES_PASSWORD=secret
      - POSTGRES_DB=noflux
    volumes:
      - noflux-db:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD", "pg_isready", "-U", "noflux"]
      interval: 10s
      start_period: 30s
volumes:
  noflux-db:
```

- `DATABASE_URL` is used to define the database connection parameters
- `RUN_MIGRATIONS=1` runs the SQL migrations automatically
- `CREATE_ADMIN`, `ADMIN_USERNAME`, `ADMIN_PASSWORD` allows us to create the first admin user, and it can be removed after the first initialization.

There are more examples in the Git repository with Traefik and Caddy: https://github.com/fiatjaf/noflux/tree/master/contrib/docker-compose

You could also configure an optional health check in your Docker Compose file:

```yaml
noflux:
  image: noflux/noflux:latest
  healthcheck:
    test: ["CMD", "/usr/bin/noflux", "-healthcheck", "auto"]
```

Make sure to take a look a the list of [configuration parameters]({{< relref configuration >}}) to customize your installation.
