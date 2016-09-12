# Create our first image.
1: Image
    $ docker images

2: Container (Instanted or Instance of Image)

Check Version
$ docker version
Let's us know API version and go version for docker daemon.

$ docker info

See where all the containers details live
`var/lib/docker` is where all `images/containers` are stored
cd `var/lib/docker/containers/<hex>`

Whats Running
$ docker ps

What has run (With no name passed, it makes up a name)
$ docker ps -a

Refer to a Container by CONTAINER_ID or NAME

## The actual container images are here:
ls `/var/lib/docker/image/aufs/imagedb/content/sha256`

# Pull an image
```
docker pull ubuntu (would be latest)
docker pull ubuntu:trusty (Or any tag listed in dockerhub)
```

"Container Layers build the docker image"

# Launch container
(i = interactive, -t = attach to terminal)
This will launch the container, but not keep it running once we exit
```
docker run -it ubuntu:xenial /bin/bash
```

```
docker ps -a
```

Grab name name of what we ran, eg 'adoring_einstein'

```
docker restart adoring_einstein
docker ps
docker attach adoring_einstein  (Logs us in)
```

## Keep the container running in Background
(disconnected/daemonized)

```
docker run -itd ubuntu:xenial /bin/bash
```

#### Run another Instance

```
docker run -itd ubuntu:xenial /bin/bash
```

## Info about the Base image
```
docker inspect ubuntu:xenial
docker ps  (See the different names)
```

## Info about Container
```
docker ps -a
docker inspect compassionate_bhaskara
docker inspect compassionate_bhaskara | grep IP
```

## Going into container

```
docker attach compassionate_bhaskara
<Enter>
```

## Stopping Containers
```
docker stop <name>
docker ps -a
```

## Searching for containers
```
docker search ruby
docker search training/sinatra
```

# Instance Examples
```
docker pull training/sinatra
docker run -it training/sinatra /bin/bash
gem
gem list --local
```

### Create a file in this instance
```
cd /root
echo "Testing" > test.txt
exit
```

### Notice new instances don't have our old items
```
docker run -it training/sinatra /bin/bash
ls /root
```

### We can reboot our old instance
```
docker ps -a
docker restart sad_bohr
docker attach sad_bohr
ls /root         ;(Our test.txt remains)
```

# Packaging a custom container
Instantiate
```
docker ps -a
docker run -it ubuntu:xenial /bin/bash
cd /root
echo "This is version 1 of our custom image" > image_version.txt
apt-get update
apt-get install telnet openssh-server

adduser test

which sshd
which telnet

cat /etc/group | grep test

docker ps -a

docker restart compassionate_cori
docker attach compassionate_cori

docker commit -m "Already installed SSH and created test user" -a "imboyus" compassionate_cori imboyus/ubuntusshd:v1

docker images

docker run -it imboyus/ubuntusshd:v1 /bin/bash
```

# Build a Dockerfile from box
```
vim Dockerfile
```

**Dockerfile**
```
# This is a ubuntu image with SSH already installed
FROM ubuntu:xenial
MAINTAINER imboyus <imboyus@gmail.com>
RUN apt-get update
RUN apt-get install -y telnet openssh-server
```

```
docker build -t="imboyus/ubuntusshdonly:v2" .
docker images
docker run -t imboyus/ubuntusshdonly:v2 /bin/bash
```

