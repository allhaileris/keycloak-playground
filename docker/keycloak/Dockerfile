ARG KEYCLOAK_IMAGE
ARG MAVEN_IMAGE

FROM $MAVEN_IMAGE as builder
RUN git clone https://github.com/daniel-frak/keycloak-user-migration.git
WORKDIR /keycloak-user-migration/
RUN cp pom.xml /tmp/ && \
    cp -r src /tmp/src
WORKDIR /tmp/
RUN mvn clean package

FROM $KEYCLOAK_IMAGE
USER root
COPY --from=builder /tmp/target/*.jar /opt/keycloak/providers/app.jar
USER 1000

ENTRYPOINT ["/opt/keycloak/bin/kc.sh"]
