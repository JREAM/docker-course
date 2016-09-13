# Dockerfile based on the latest CentOS 7 image - non-privileged user entry
FROM centos:latest
MAINTAINER imboyus@gmail.com

RUN useradd -ms /bin/bash user

# We are making this up for example
RUN echo "EXPORT 192.168.0.0/24" >> /etc/exports.list

RUN yum update -y
RUN yum install -y net-tools wget


# We have to accepot certificate from Orace
RUN cd ~ && wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u60-b27/jre-8u60-linux-x64.rpm"

# localinstall instead of RPM because it may have dependencies
RUN yum localinstall -y ~/jre-8u60-linux-x64.rpm


USER user

# Remember we are now the "user" User, so commands below are executed as him
RUN cd ~ && echo "export JAVA_HOME=/usr/java/jdk1.8.0/jre" >> /home/user/.bashrc

# Systemwide Enviroment Variable
ENV JAVA_BIN /usr/java/jdk1.8.0/jre