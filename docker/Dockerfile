# Use the official Jenkins LTS image from the Docker Hub
FROM jenkins/jenkins:lts

# Skip the initial setup
ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false

# Switch to root user to install Docker
USER root

# Install required packages and Docker
RUN apt-get update && \
    apt-get install -y \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg2 \
        lsb-release \
        software-properties-common && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
    add-apt-repository \
        "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" && \
    apt-get update && \
    apt-get install -y docker-ce-cli && \
    usermod -aG docker jenkins && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Switch back to the jenkins user
USER jenkins

# Expose the Jenkins web UI port
EXPOSE 8080

# Expose the Jenkins agent port
EXPOSE 50000

# Specify the default command to run Jenkins
CMD ["jenkins"]
