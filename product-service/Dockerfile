# ---- Build Stage ----
FROM maven:3.9-eclipse-temurin-17 AS builder
WORKDIR /app

# Copy project files
COPY pom.xml .
COPY . .

# Build the project (skip tests for speed)
RUN mvn -B clean package -DskipTests

# ---- Runtime Stage ----
FROM eclipse-temurin:17-jre-jammy
WORKDIR /app

# Copy built jar
COPY --from=builder /app/target/*.jar app.jar

# Expose application port (overridden by env if needed)
ENV SERVER_PORT=8080
EXPOSE ${SERVER_PORT}

# Run application
ENTRYPOINT ["sh", "-c", "java -jar /app/app.jar"]
