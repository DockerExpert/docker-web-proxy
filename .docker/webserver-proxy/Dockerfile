FROM nginx:alpine

RUN apk update && apk upgrade

RUN apk add --no-cache bash

COPY conf/vhost.conf  /etc/nginx/conf.d/vhost.conf
COPY conf/domain.crt /etc/nginx/domain.crt
COPY conf/domain.key /etc/nginx/domain.key