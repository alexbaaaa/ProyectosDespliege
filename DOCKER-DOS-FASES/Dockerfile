# Construir .war
FROM maven:3.9.9-eclipse-temurin-17 as build
WORKDIR /app
RUN mvn clean package 

# Construir imagen con tomcat
FROM tomcat:11.0.2-jdk17-temurin
COPY --from=build /app/target/my-webapp.war /usr/tomcat/webapps/ROOT.war