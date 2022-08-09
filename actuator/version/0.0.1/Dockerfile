FROM anapsix/alpine-java:8_server-jre_unlimited

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

ARG JASYPT_ENCRYPTOR_PASSWORD=""
ENV JAVA_OPTS=""
ARG COMMON_SERVICE_IP=""

EXPOSE 8080

COPY app.jar app.jar

RUN echo -e "#!/bin/sh\njava ${JAVA_OPTS} -Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom -DJASYPT_ENCRYPTOR_PASSWORD=${JASYPT_ENCRYPTOR_PASSWORD} -Dsun.net.httpserver.nodelay=true -jar ./app.jar" > ./entrypoint.sh
RUN chmod +x ./entrypoint.sh

ENTRYPOINT ["./entrypoint.sh"]
