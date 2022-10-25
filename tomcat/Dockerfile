FROM bitnami/git:latest as git
WORKDIR /work
RUN git clone --depth=1 https://github.com/Azure-Samples/pet-clinic-war.git && \
    chmod +x pet-clinic-war/mvnw


FROM amazoncorretto:11-alpine as builder
COPY --from=git /work/pet-clinic-war /work/pet-clinic-war
WORKDIR /work/pet-clinic-war
RUN ./mvnw package


FROM tomcat:9.0.68-jdk11-corretto
COPY --from=builder /work/pet-clinic-war/target/spring-petclinic-2.3.1.BUILD-SNAPSHOT.war /usr/local/tomcat/webapps/ROOT.war
ADD https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/download/v1.19.1/opentelemetry-javaagent.jar /opt/opentelemetry-javaagent.jar
