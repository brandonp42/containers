
### How to use this:

Create the network:

```
docker network create jenkins
```

Start the Jenkins server:

```bash
docker run \
  --name jenkins-server \
  --restart=on-failure \
  --detach \
  --network jenkins \
  --publish 8080:8080 \
  --volume jenkins-data:/var/jenkins_home \
  docker.io/jenkins/jenkins:2.419-rhel-ubi9-jdk17
```

Start the Jenkins agent:

```bash
AGENT_NAME=agent-podman-1

docker run \
  --name ${AGENT_NAME} \
  --restart=on-failure \
  --detach \
  --network jenkins \
  --privileged \
  ghcr.io/brandonp42/containers/jenkins-inbound-agent-podman-jdk17:latest \
  -url http://jenkins-server:8080 __put_agent_secret_here__ ${AGENT_NAME}
```
