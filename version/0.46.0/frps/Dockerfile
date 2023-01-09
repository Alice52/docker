FROM amd64/alpine:3.15

LABEL maintainer="alice52 <zzhang_xz@163.com>"

ARG FRP_CLIENT_ADMIN_PORT
ARG FRP_PWD
ARG FRP_SERVER_ADDR
ARG FRP_SERVER_ADMIN_PORT
ARG FRP_SERVER_BIND_PORT
ARG FRP_TOKEN
ARG FRP_USER

ENV FRP_VERSION 0.46.0

RUN cd /root \
  &&  wget --no-check-certificate -c https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_amd64.tar.gz \
  &&  tar zxvf frp_${FRP_VERSION}_linux_amd64.tar.gz  \
  &&  cd frp_${FRP_VERSION}_linux_amd64/ \
  &&  cp frps /usr/bin/ \
  &&  mkdir -p /etc/frp \
  &&  cp frps.ini /etc/frp \
  &&  cd /root \
  &&  rm frp_${FRP_VERSION}_linux_amd64.tar.gz \
  &&  rm -rf frp_${FRP_VERSION}_linux_amd64/

COPY ./frps.ini /etc/frp/frps.ini

RUN echo -e "#!/bin/sh\n export FRP_CLIENT_ADMIN_PORT=${FRP_CLIENT_ADMIN_PORT} \n export FRP_PWD=${FRP_PWD} \n export FRP_SERVER_ADDR=${FRP_SERVER_ADDR} \n export FRP_SERVER_ADMIN_PORT=${FRP_SERVER_ADMIN_PORT} \n export FRP_SERVER_BIND_PORT=${FRP_SERVER_BIND_PORT} \n export FRP_TOKEN=${FRP_TOKEN} \n export FRP_USER=${FRP_USER} \n /usr/bin/frps -c /etc/frp/frps.ini" > ./entrypoint.sh

RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

