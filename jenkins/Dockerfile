FROM jenkins/jenkins:lts-jdk17
USER root

RUN apt-get update && apt-get install -y lsb-release

RUN curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list

RUN apt-get update && \
    apt-get install -y docker-ce-cli && \
    apt-get install -y curl && \
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/$(dpkg --print-architecture)/kubectl" && \
    install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl && \
    rm kubectl

RUN if ! apt-get install -y docker-ce-cli; then \
        echo "Falling back to manual Docker CLI installation"; \
        curl -fsSL https://download.docker.com/linux/static/stable/$(uname -m | sed 's/x86_64/x86_64/')/docker-20.10.23.tgz | tar -xzC /usr/local/bin --strip-components=1; \
    fi

RUN usermod -aG docker jenkins && \
    chmod 666 /var/run/docker.sock || true
RUN mkdir -p /var/jenkins_home && \
    chown -R 1000:1000 /var/jenkins_home && \
    chmod -R 755 /var/jenkins_home

USER jenkins