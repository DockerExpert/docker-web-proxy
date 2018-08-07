FROM httpd:alpine

RUN apk update && apk upgrade

RUN apk add --no-cache bash

COPY conf/httpd.conf /usr/local/apache2/conf/httpd.conf