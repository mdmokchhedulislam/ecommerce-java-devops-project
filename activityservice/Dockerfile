# ---- Stage 1: Build ----
FROM maven:3.9.9-eclipse-temurin-17 AS build

WORKDIR /app

# Copy pom.xml first for dependency caching
COPY pom.xml .
RUN mvn clean install -DskipTests

# Copy source code and build jar
COPY src ./src
RUN mvn clean package -DskipTests

# ---- Stage 2: Runtime ----
FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

# Copy the built jar from build stage
COPY --from=build /app/target/*.jar app.jar

# Expose the activity-service port (update if needed)
EXPOSE 8082

# Run the jar
ENTRYPOINT ["java", "-jar", "app.jar"]
