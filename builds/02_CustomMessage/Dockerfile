# Dockerfile based on the latest CentOS 7 image - non-privileged user entry
FROM centos:latest
MAINTAINER imboyus@gmail.com

RUN useradd -ms /bin/bash user

# We are making this up for example
RUN echo "EXPORT 192.168.0.0/24" >> /etc/exports.list

USER user


