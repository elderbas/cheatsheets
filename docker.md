---
title: Docker CLI
category: Devops
layout: 2018/sheet
---

## `docker container`

### `ls -a`

See all containers (including stopped ones). Only use `ls` if you only want to see active containers

-----

### `run`

`docker container run --publish 80:80 --detach nginx`

all traffic directed to the host's port (left) 80 is directed to the container's port 80 (right)

-----

#### `run -it`

open an interactive shell prompt into a container.

`-t` gives us the access into the container
`-i` keeps it open

-----

#### `rm`

`docker container rm -f $(docker container ls -aq)`

remove all containers, including dead ones

-----

#### `start`

Usage:	docker container start [OPTIONS] CONTAINER [CONTAINER...]

Start one or more stopped containers

























# OLD


Manage images
-------------

### `docker build`

```yml
docker build [options] .
  -t "app/container_name"    # name
```

Create an `image` from a Dockerfile.


### `docker run`

```yml
docker run [options] IMAGE
  # see `docker create` for options
```

Run a command in an `image`.

Manage containers
-----------------

### `docker create`

```yml
docker create [options] IMAGE
  -a, --attach               # attach stdout/err
  -i, --interactive          # attach stdin (interactive)
  -t, --tty                  # pseudo-tty
      --name NAME            # name your image
  -p, --publish 5000:5000    # port map
      --expose 5432          # expose a port to linked containers
  -P, --publish-all          # publish all ports
      --link container:alias # linking
  -v, --volume `pwd`:/app    # mount (absolute paths needed)
  -e, --env NAME=hello       # env vars
```

#### Example

```
$ docker create --name app_redis_1 \
  --expose 6379 \
  redis:3.0.2
```

Create a `container` from an `image`.

### `docker exec`

```yml
docker exec [options] CONTAINER COMMAND
  -d, --detach        # run in background
  -i, --interactive   # stdin
  -t, --tty           # interactive
```

#### Example

```
$ docker exec app_web_1 tail logs/development.log
$ docker exec -t -i app_web_1 rails c
```

Run commands in a `container`.


### `docker start`

```yml
docker start [options] CONTAINER
  -a, --attach        # attach stdout/err
  -i, --interactive   # attach stdin

docker stop [options] CONTAINER
```

Start/stop a `container`.


### `docker ps`

```
$ docker ps
$ docker ps -a
$ docker kill $ID
```

Manage `container`s using ps/kill.

Images
------

### `docker images`

```sh
$ docker images
  REPOSITORY   TAG        ID
  ubuntu       12.10      b750fe78269d
  me/myapp     latest     7b2431a8d968
```

```sh
$ docker images -a   # also show intermediate
```

Manages `image`s.

### `docker rmi`

```yml
docker rmi b750fe78269d
```

Deletes `image`s.

Also see
--------

 * [Getting Started](http://www.docker.io/gettingstarted/) _(docker.io)_
