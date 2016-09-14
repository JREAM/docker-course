# Docker Cheatsheet

```
docker images
docker ps  ; Show running containers
docker ps -a ; Show all containers

docker rm <container(name|id)> ; Remove a container
docker rmi <image(name|id)> ; Remove an image
docker rmi -f <image(name|id)> ; Force Removal if running

docker run
docker exec
docker attach

docker build
docker create
docker inspect

docker network

docker start
docker stop
docker restart

docker login   ; DockerHub Account
docker logout  ; DockerHub Account
docker push <image(name:tag)> ; To Docker Account

docker stats

docker tag
docker rename

docker top <container(name|id)>

docker version
docker volume
```