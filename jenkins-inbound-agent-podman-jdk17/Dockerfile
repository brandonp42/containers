FROM docker.io/jenkins/inbound-agent:latest-jdk17

USER root

RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get install -y curl podman wget \
    && wget https://github.com/aquasecurity/trivy/releases/download/v0.50.1/trivy_0.50.1_Linux-64bit.deb \
    && dpkg -i trivy_0.50.1_Linux-64bit.deb \
    && rm trivy_0.50.1_Linux-64bit.deb \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sSfL https://raw.githubusercontent.com/anchore/grype/main/install.sh | sh -s -- -b /usr/local/bin

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
