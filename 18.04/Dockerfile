FROM       ubuntu:18.04
MAINTAINER Priests of the Temple of Syrinx "https://github.com/orgs/TemplesOfSyrinx/teams/priests"

# Set which versions to use
ENV OPENSSH_SERVER_VERSION 1:7.6p1-4

# Update and install as root
RUN apt-get update && \
    apt-get install -y \
        openssh-server \
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* \
           /tmp/* \
           /var/tmp/*

RUN mkdir /var/run/sshd

RUN echo 'root:root' |chpasswd

RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

EXPOSE 22

CMD    ["/usr/sbin/sshd", "-D"]
