# Dockerfile based on the latest CentOS 7 image - non-privileged user entry
FROM centos:latest
MAINTAINER imboyus@gmail.com

RUN useradd -ms /bin/bash user

# If I instantiate this container, I should get this message
CMD "echo" "This is a custom container message"

USER user
