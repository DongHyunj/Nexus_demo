FROM gradle:8-jdk17-alpine AS builder
WORKDIR /app
COPY backend/gradle ./gradle
COPY backend/gradlew backend/build.gradle backend/settings.gradle ./
RUN chmod +x ./gradlew && ./gradlew dependencies --no-daemon || true
COPY backend/src ./src
RUN ./gradlew bootJar -x test --no-daemon

FROM eclipse-temurin:17-jre-alpine
COPY --from=builder /app/build/libs/*.jar /app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app.jar"]
