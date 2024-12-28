
# Spring Boot Docker Setup

This README outlines the steps to containerize a Spring Boot application using Docker.

## Dockerfile Overview

The following Dockerfile is used to create a lightweight Docker image for a Spring Boot application:

```Dockerfile
FROM java:8-jdk-alpine

# Copy the packaged JAR file into the Docker image
COPY ./target/spring-boot-docker-app.jar /usr/app/

# Set the working directory inside the container
WORKDIR /usr/app

# Ensure the JAR file is executable by touching it
RUN sh -c 'touch spring-boot-docker-app.jar'

# Set the entry point to run the application
ENTRYPOINT ["java","-jar","spring-boot-docker-app.jar"]
```

---

## How to Build and Run the Docker Image

### 1. Build the Spring Boot Application
Ensure that the Spring Boot application is packaged as a JAR file by running the following command:

```bash
mvn clean package
```

### 2. Build the Docker Image
Execute the following command to build the Docker image:

```bash
docker build -t spring-boot-docker-app .
```

### 3. Run the Docker Container
Run the container using the following command:

```bash
docker run -p 8080:8080 spring-boot-docker-app
```

---

## Key Points:
- **Base Image**: `java:8-jdk-alpine` is a lightweight Java runtime environment.
- **Working Directory**: The JAR file is copied to `/usr/app`.
- **Entry Point**: The container runs the application by executing `java -jar spring-boot-docker-app.jar`.
- **Port Mapping**: Ensure port 8080 is exposed and mapped to the host machine.

---

## Verifying the Container
To verify if the container is running, use the following command:

```bash
docker ps
```

Visit `http://localhost:8080` to access the Spring Boot application.

---

## Troubleshooting
- If the application does not start, check the logs using:

```bash
docker logs <container_id>
```

- Ensure that the JAR file is correctly packaged and present in the `target/` directory.

Happy containerizing!


