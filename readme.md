# Docker Course

Definitions:
- Image: Pre-built or static package (Like OOP Class)
- Container: Instantiated instance of an Image (Like OOP Instance)

# Create our first image.
```
docker images
```

Check Version
$ docker version
Let's us know API version and go version for docker daemon.

$ docker info

See where all the containers details live
`var/lib/docker` is where all `images/containers` are stored
cd `var/lib/docker/containers/<hex>`

## Whats Running
```
docker ps
```

## What Has Run
Notice that it will make a random name to re-use an instance that's stopped.
```
docker ps -a
```

## Where Images are Located
On the system you are running docker look in:
```
ls `/var/lib/docker/image/aufs/imagedb/content/sha256`
```

## Pull an image
```
docker pull ubuntu          (would be latest)
docker pull ubuntu:trusty   (Or any tag listed in dockerhub)
```

_"Container Layers build the docker image"_

## Launch container
- `-i`    interactive
- `-t`    attach to terminal
- `-d`    detached/daemonized

This will launch the container, but it will not keep running once we exit
```
docker run -it ubuntu:xenial /bin/bash
exit
```

You can see here after you exit
```
docker ps
docker ps -a    (But it will appear here)
```

## Relaunch a Container Instance
Grab name name of what we ran, eg 'adoring_einstein' by doing:

```
docker ps -a                    (Look for the friendly name)
docker restart adoring_einstein
docker ps
docker attach adoring_einstein  (Logs us in)
```

## Keep the Container running in Background
```
docker run -itd ubuntu:xenial /bin/bash
```

#### Run another Instance
If you make changes to instance one, instance two is not affected.
```
docker run -itd ubuntu:xenial /bin/bash
```

## Get Base Image Info
```
docker inspect ubuntu:xenial
docker ps  (See the different names if you launched two)
```

## Get Container Info
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

## Searching for Images
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

