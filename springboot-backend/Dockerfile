#STAGE: - BUILD the app
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app

COPY pom.xml .
#download all dependencies now so that there is no need for internet later
RUN mvn -B dependency:go-offline

COPY src ./src

#make compiled artifact(.JAR) and place in /target. -B (non interactive mode)
RUN mvn -B package -DskipTests

#STAGE:2 - RUN the app
FROM eclipse-temurin:17-jre
WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT [ "java", "-jar", "app.jar" ]