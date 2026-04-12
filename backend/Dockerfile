## Java app build stage 1 -> .jar using maven

FROM maven:3.9-eclipse-temurin-17 AS builder
WORKDIR /backend 

COPY pom.xml . 

RUN mvn dependency:go-offline

COPY /src ./src/

RUN mvn package -DskipTests

## stage 2 tests

FROM builder AS test
RUN mvn test

## JRE starts .jar stage 3

FROM eclipse-temurin:17-jre AS final 

WORKDIR /backend

EXPOSE 8080 

COPY --from=test /backend/target/*.jar backend.jar

ENTRYPOINT ["java", "-jar", "backend.jar"]