# Use the official Jenkins LTS image from the Docker Hub
FROM jenkins/jenkins:lts

# Skip the initial setup
ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false

# Install Docker inside the Jenkins container
USER root
RUN apt-get update && \
    apt-get install -y apt-transport-https ca-certificates curl gnupg2 software-properties-common && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" && \
    apt-get update && \
    apt-get install -y docker-ce-cli && \
    usermod -aG docker jenkins

# Switch back to the jenkins user
USER jenkins

# Expose the Jenkins web UI port
EXPOSE 8080

# Specify the default command to run Jenkins
CMD ["jenkins"]

