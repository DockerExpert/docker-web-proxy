FROM php:7.2-fpm-alpine3.7

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
    libpng \
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

## configure libraries
RUN docker-php-ext-configure gd \
    --enable-gd-native-ttf \
    --with-freetype-dir=/usr/include/freetype2 \
    --with-jpeg-dir=/usr/lib/x86_64-linux-gnu/ \
    && docker-php-ext-configure hash --with-mhash

## install required extensions
RUN docker-php-ext-install \
    bcmath \
    mysqli \
    gd \
    intl \
    pdo_mysql \
    opcache \
    xsl \
    zip \
    soap

# add XDebug for the dev env build
#RUN pecl install xdebug  \
#    && docker-php-ext-enable xdebug

ENV TZ=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN pecl install -o -f redis \
&&  rm -rf /tmp/pear \
&&  docker-php-ext-enable redis

COPY /conf/php-ini-overrides.ini  /usr/local/etc/php/conf.d/php-ini-overrides.ini
#COPY /conf/xdebug.ini  /usr/local/etc/php/conf.d/xdebug.ini

#RUN set -x \
#    && deluser www-data \
#    && addgroup -g 500 -S www-data \
#    && adduser -u 500 -D -S -G www-data www-data

# add mhsendmail (sendmail is forced to use smtp)
RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.10.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail

# Set Timezone
ENV TZ=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ENV COMPOSER_ALLOW_SUPERUSER=1

# Install Ioncube Loader for php 7.0
# RUN wget http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz \
#    && tar xvfz ioncube_loaders_lin_x86-64.tar.gz \
#    && cp ioncube/ioncube_loader_lin_7.0.so /usr/local/lib/php/extensions/no-debug-non-zts-20151012/ \
#    && rm -rf ioncube \
#    && cd /usr/local/etc/php/conf.d \
#    && touch 00-ioncube.ini \
#    && echo "zend_extension=ioncube_loader_lin_7.0.so" > 00-ioncube.ini

# Install Ioncube Loader for php 7.1
# RUN wget http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz \
#    && tar xvfz ioncube_loaders_lin_x86-64.tar.gz \
#    && cp ioncube/ioncube_loader_lin_7.1.so /usr/local/lib/php/extensions/no-debug-non-zts-20160303/ \
#    && rm -rf ioncube \
#    && cd /usr/local/etc/php/conf.d \
#    && touch 00-ioncube.ini \
#    && echo "zend_extension=ioncube_loader_lin_7.1.so" > 00-ioncube.ini

# Install Ioncube Loader for php 7.2
# RUN wget https://downloads.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz
#    && tar -xvf ioncube_loaders_lin_x86-64.tar.gz
#    && cp ioncube/ioncube_loader_lin_7.2.so  /usr/local/lib/php/extensions/no-debug-non-zts-20170718/ \
#    && rm -rf ioncube \
#    && cd /usr/local/etc/php/conf.d \
#    && touch 00-ioncube.ini \
#    && echo "zend_extension=ioncube_loader_lin_7.2.so" > 00-ioncube.ini

RUN apk del \
    icu \
    go \
    git \
    libc-dev \
    libxslt-dev \
    libmcrypt-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng \
    libpng-dev \
    make \
    $PHPIZE_DEPS \
    zlib-dev \
    icu-dev \
    g++


