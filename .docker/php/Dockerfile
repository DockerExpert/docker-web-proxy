FROM php:7.0-fpm-alpine

RUN apk update && apk upgrade

RUN apk add --no-cache bash

RUN docker-php-ext-install pdo_mysql

#COPY php/conf/php-ini-overrides.ini  /usr/local/etc/php/conf.d/php-ini-overrides.ini