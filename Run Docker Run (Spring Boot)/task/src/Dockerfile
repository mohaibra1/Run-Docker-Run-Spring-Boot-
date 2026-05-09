# Stage 1: Build stage
FROM eclipse-temurin:21-jdk AS build
WORKDIR /app

# 1. Transfer the Gradle Wrapper files
COPY gradlew gradlew.bat ./

# 2. Transfer the gradle folder into the gradle folder
COPY gradle ./gradle

# 3. Transfer the Gradle project files
COPY build.gradle settings.gradle ./

# 4. Transfer the src folder
COPY src ./src

# 5. Ensure Gradle Wrapper has executable permissions
RUN chmod +x gradlew

# 6. Build the application
RUN ./gradlew bootJar --no-daemon

# Stage 2: Package stage
FROM eclipse-temurin:21-jre
WORKDIR /app

# 7. Copy the JAR file generated in the build stage
# Note: The filename must match the one specified in your objectives
COPY --from=build /app/build/libs/hyper-web-app-0.0.1-SNAPSHOT.jar app.jar

# 8. Expose port 8080
EXPOSE 8080

# 9. Set the entry point
ENTRYPOINT ["java", "-jar", "app.jar"]
