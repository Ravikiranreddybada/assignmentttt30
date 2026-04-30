FROM jenkins/jenkins:lts

USER root

# Install Docker CLI
RUN apt-get update && apt-get install -y apt-transport-https ca-certificates curl gnupg2 software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
RUN apt-get update && apt-get install -y docker-ce-cli

# Install Node.js (v20)
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash -
RUN apt-get install -y nodejs

# Add jenkins user to docker group (id 999 is common for docker group on many systems, but we'll use the socket's group at runtime or just run as root for simplicity in this dev setup)
# However, the most reliable way in Docker-out-of-Docker is to ensure the jenkins user can access the mounted /var/run/docker.sock

USER jenkins
