FROM php:7.0-fpm-alpine

RUN apk update && apk upgrade

RUN apk add --no-cache --virtual build-dependencies \
    go \
    git \
    libc-dev \
    bash \
    libxslt-dev \
    libmcrypt-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev

RUN set -xe \
    && apk add --update \
        icu \
    && apk add --no-cache --virtual .php-deps \
        make \
    && apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        zlib-dev \
        icu-dev \
        g++

# configure libraries
RUN docker-php-ext-configure gd \
    --enable-gd-native-ttf \
    --with-freetype-dir=/usr/include/freetype2 \
    --with-jpeg-dir=/usr/lib/x86_64-linux-gnu/ \
    && docker-php-ext-configure hash --with-mhash

# install required extensions
RUN docker-php-ext-install \
    bcmath \
    mysqli \
    pdo_mysql \
    mcrypt \
    opcache \
    xsl \
    zip \
    soap

COPY /conf/php-ini-overrides.ini  /usr/local/etc/php/conf.d/php-ini-overrides.ini

RUN set -x \
    && deluser www-data \
    && addgroup -g 500 -S www-data \
    && adduser -u 500 -D -S -G www-data www-data

# add mhsendmail (sendmail is forced to use smtp)
RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.10.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail

# add XDebug for the dev env build
RUN pecl install xdebug  \
    && docker-php-ext-enable xdebug

# configure app folder
ENV WORK_DIR ${WORK_DIR:-/var/www}
WORKDIR $WORK_DIR

# Set Timezone
ENV TZ=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install Ioncube Loader for php 7.0
RUN wget http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz \
    && tar xvfz ioncube_loaders_lin_x86-64.tar.gz \
    && cp ioncube/ioncube_loader_lin_7.0.so /usr/local/lib/php/extensions/no-debug-non-zts-20151012/ \
    && rm -rf ioncube \
    && cd /usr/local/etc/php/conf.d \
    && touch 00-ioncube.ini \
    && echo "zend_extension=ioncube_loader_lin_7.0.so" > 00-ioncube.ini

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ENV COMPOSER_ALLOW_SUPERUSER=1