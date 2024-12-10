# Stage 1: Build the application using Maven
FROM openjdk:17-jdk-slim AS build

# Set environment variables for Maven
ENV MAVEN_VERSION=3.8.8
ENV M2_HOME=/opt/apache-maven-$MAVEN_VERSION
ENV PATH="$M2_HOME/bin:$PATH"

# Install wget and other necessary tools
RUN apt-get update && \
    apt-get install -y wget vim && \ 
    apt-get clean
RUN apt-get update && \
    apt-get install -y default-mysql-client && \
    rm -rf /var/lib/apt/lists/*


# Download and install Maven
RUN wget https://dlcdn.apache.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz && \
    tar -xvf apache-maven-$MAVEN_VERSION-bin.tar.gz && \
    mv apache-maven-$MAVEN_VERSION /opt/ && \
    rm apache-maven-$MAVEN_VERSION-bin.tar.gz

# Set working directory for building the application
WORKDIR /app


# Copy the JAR file from the build stage to the final image
COPY target/springboot-backend-0.0.1-SNAPSHOT.jar app.jar
COPY src/main/resources/application.properties application.properties

# Expose the port that your application will listen on
EXPOSE 8080

# Run the Spring Boot application
CMD ["java", "-jar", "app.jar"]
#CMD ["tail", "-f", "/dev/null"]
