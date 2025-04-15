FROM maven:3.9.4-eclipse-temurin-21 AS builder
WORKDIR /app
ENV MAVEN_CONFIG=/var/maven/.m2
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn clean package -DskipTests
FROM eclipse-temurin:21-jdk-jammy
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
