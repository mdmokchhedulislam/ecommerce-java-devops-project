# ---- Stage 1: Build ----
FROM maven:3.9.9-eclipse-temurin-17 AS build

# Set working directory
WORKDIR /app

# Copy pom.xml and download dependencies (layer caching)
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copy source code and build
COPY src ./src
RUN mvn clean package -DskipTests

# ---- Stage 2: Runtime ----
FROM eclipse-temurin:17-jre-alpine

# Set working directory
WORKDIR /app

# Copy the built JAR from build stage
COPY --from=build /app/target/aiservice-0.0.1-SNAPSHOT.jar aiservice.jar

# Expose the port
EXPOSE 8083

# Run the application
ENTRYPOINT ["java","-jar","aiservice.jar"]
