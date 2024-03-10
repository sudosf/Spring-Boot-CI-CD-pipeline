# Use a Maven image as the base image for the build stage
FROM maven:latest AS build

# Set the working directory in the container
WORKDIR /app

# Copy the pom.xml file to the container
COPY pom.xml .

# Copy the rest of the application code
COPY src ./src

# Build the application using Maven
RUN mvn clean package

# Use an OpenJDK image with Java 21 as the base image for the final stage
FROM adoptopenjdk/openjdk21:jdk-slim AS runtime

# Set the working directory in the container
WORKDIR /app

# Copy the built JAR file from the build stage to the final stage
COPY --from=build /app/target/beanchat-app.jar app.jar

# Expose the port that the Spring Boot application listens on
EXPOSE 8080

# Specify the command to run the Spring Boot application
ENTRYPOINT ["java", "-jar", "app.jar"]