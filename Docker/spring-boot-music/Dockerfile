FROM levep79/jdk-alpine:latest
WORKDIR /app
COPY ./artifacts/spring-music.jar /spring-music.jar
EXPOSE 8080
CMD ["/usr/bin/java", "-jar", "-Dspring.profiles.active", "/spring-music.jar"]
