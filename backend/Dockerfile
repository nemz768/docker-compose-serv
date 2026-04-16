## Java app build stage 1 -> .jar using maven

FROM maven:3.9-eclipse-temurin-17 AS build
WORKDIR /backend 

COPY pom.xml . 

RUN mvn dependency:go-offline

COPY /src ./src/

RUN mvn package -DskipTests

## JRE starts .jar stage 2

FROM eclipse-temurin:17-jre-alpine AS final 

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

WORKDIR /backend

COPY --from=build /backend/target/*.jar backend.jar

RUN chown appuser:appgroup backend.jar

USER appuser

EXPOSE 8080 

ENTRYPOINT ["java", "-jar", "backend.jar"]
