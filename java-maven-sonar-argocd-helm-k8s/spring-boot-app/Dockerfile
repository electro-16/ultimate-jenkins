# You can change this base image to anything else
# But make sure to use the correct version of Java
# Base image: Maven + Java 17
FROM maven:3.9.9-eclipse-temurin-17

LABEL maintainer="your-name"
LABEL description="Minimal DevOps CI Executor Image - Java17 + Maven + Docker + kubectl + Helm"

# Install required packages
RUN apt-get update && \
    apt-get install -y \
        docker.io \
        curl \
        git \
        bash \
        ca-certificates \
        unzip && \
    rm -rf /var/lib/apt/lists/*

# Install kubectl
RUN curl -LO "https://dl.k8s.io/release/$(curl -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" && \
    install -m 0755 kubectl /usr/local/bin/kubectl && \
    rm kubectl

# Install Helm
RUN curl -fsSL https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

# Verify installations (fail build if missing)
RUN java -version && \
    mvn -version && \
    docker --version && \
    kubectl version --client && \
    helm version

# Default shell for Jenkins
# CMD ["bash"]

#FROM eclipse-temurin:17-jdk-alpine

#RUN apt-get update && \
 #   apt-get install -y docker.io && \
 #   apt-get clean

# Simply the artifact path
ARG artifact=target/spring-boot-web.jar

WORKDIR /opt/app

COPY ${artifact} app.jar

# This should not be changed
ENTRYPOINT ["java","-jar","app.jar"]
