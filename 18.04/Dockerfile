FROM       ubuntu:18.04
MAINTAINER Priests of the Temple of Syrinx "https://github.com/orgs/TemplesOfSyrinx/teams/priests"

# Set which versions to use
ENV OPENSSH_SERVER_VERSION 1:7.6p1-4ubuntu0.3
ENV GIT_VERSION 1:2.17.1-1ubuntu0.7

# Update and install as root
RUN apt-get update && \
    apt-get install --no-install-recommends -y \
        openssh-server="$OPENSSH_SERVER_VERSION" \
        git="$GIT_VERSION" \
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* \
           /tmp/* \
           /var/tmp/*

RUN mkdir /var/run/sshd

RUN echo 'root:root' |chpasswd

RUN sed -ri 's/^#?(PermitRootLogin)\s+.*/\1 yes/' /etc/ssh/sshd_config
RUN sed -ri 's/^(UsePAM\s+.*)/#\1/g' /etc/ssh/sshd_config

EXPOSE 22

CMD    ["/usr/sbin/sshd", "-D"]
