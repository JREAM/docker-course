# Dockerfile based on the latest CentOS 7 image
FROM centos:latest
MAINTAINER imboyus@gmail.com

RUN useradd -ms /bin/bash user

# This will happen no matter what container is based upon this image
ENTRYPOINT echo "This command will display this message on EVERY container that is run from it"

USER user
