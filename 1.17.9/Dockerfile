FROM nginx:1.17.9

RUN apt-get update
RUN apt-get install ipvsadm -y
RUN apt-get install net-tools -y

COPY ./conf/nginx.conf/nginx.conf /etc/nginx/nginx.conf
COPY ./conf/conf.d/default.conf /etc/nginx/conf.d/default.conf
