FROM openjdk:8u212-jre-slim-stretch
VOLUME /tmp

ARG JASYPT_ENCRYPTOR_PASSWORD=""
ARG COMMON_SERVICE_IP=""
ARG ARTHAS_VERSION=""

ADD app.jar app.jar
RUN sh -c 'touch /app.jar'
ENV JAVA_OPTS=""
EXPOSE 8080
ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -DCOMMON_SERVICE_IP=${COMMON_SERVICE_IP} -DJASYPT_ENCRYPTOR_PASSWORD=${JASYPT_ENCRYPTOR_PASSWORD} -jar /app.jar"]
