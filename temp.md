
```Dockerfile
# Stage 1: Build the application
FROM maven:3.8.6-openjdk-18 AS builder

WORKDIR /app

# Copy the pom.xml and download dependencies
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copy the source code and build the application
COPY src ./src
RUN mvn package -DskipTests

# Stage 2: Create the final image
FROM gcr.io/distroless/java17-debian12

# Copy the jar from the builder stage
COPY --from=builder /app/target/todo-1.0.0.jar /todo-1.0.0.jar
EXPOSE 8080

# Run application with java -jar
ENTRYPOINT ["java", "-jar", "/todo-1.0.0.jar"]
```