FROM docker.io/jenkins/inbound-agent:latest-jdk17

USER root

RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get install -y podman \
    && rm -rf /var/lib/apt/lists/*

RUN echo jenkins:10000:5000 > /etc/subuid; \
    echo jenkins:10000:5000 > /etc/subgid;

VOLUME /var/lib/containers
RUN mkdir -p /home/jenkins/.local/share/containers
RUN mkdir -p /home/jenkins/.config
RUN chown jenkins:jenkins -R /home/jenkins
VOLUME /home/jenkins/.local/share/containers

# https://raw.githubusercontent.com/containers/libpod/master/contrib/podmanimage/stable/containers.conf
ADD containers.conf /etc/containers/containers.conf
# https://raw.githubusercontent.com/containers/libpod/master/contrib/podmanimage/stable/podman-containers.conf
ADD podman-containers.conf /home/podman/.config/containers/containers.conf

# chmod containers.conf
RUN chmod 644 /etc/containers/containers.conf;

USER jenkins

