FROM nginx:alpine

RUN apk update && apk upgrade

RUN apk add --no-cache bash

COPY conf/webserver-proxy.conf  /etc/nginx/conf.d/webserver-proxy.conf
COPY conf/domain.crt /etc/nginx/domain.crt
COPY conf/domain.key /etc/nginx/domain.key