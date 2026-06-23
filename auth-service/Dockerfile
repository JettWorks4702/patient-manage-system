#image for jdk 21 and maven build for building code
FROM maven:3.9.9-eclipse-temurin-21 AS builder

#working directory
WORKDIR /app

#copy pom.xml to working directory
COPY pom.xml .

#cache dependencies unless change has been detected
RUN mvn dependency:go-offline -B

#copy all the src code to working directory
COPY src ./src

#we have whole dependencies and code and we have to make a build and jar it
RUN mvn clean package

FROM eclipse-temurin:21-jdk AS runner

WORKDIR /app

COPY --from=builder ./app/target/auth-service-0.0.1-SNAPSHOT.jar ./app.jar

EXPOSE 4005

ENTRYPOINT ["java", "-jar", "app.jar"]



