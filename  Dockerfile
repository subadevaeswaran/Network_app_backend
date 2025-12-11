# Start from a lightweight OpenJDK image
FROM eclipse-temurin:17-jdk-alpine

# Set working directory inside the container
WORKDIR /app

# Copy the Gradle/Maven wrapper and build files first (if using Maven, adjust accordingly)
COPY pom.xml .
COPY mvnw .
COPY .mvn .mvn

# Download dependencies first (caching layer)
RUN ./mvnw dependency:go-offline -B

# Copy the source code
COPY src ./src

# Build the Spring Boot application
RUN ./mvnw package -DskipTests

# Expose the port (Render will map PORT environment variable)
EXPOSE 8080

# Set environment variable for Spring Boot to use Render's port
ENV SERVER_PORT=${PORT}

# Run the JAR
CMD ["java", "-jar", "target/NetworkApp-0.0.1-SNAPSHOT.jar"]
