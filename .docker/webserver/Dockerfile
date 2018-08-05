FROM webdevops/php-apache-dev:7.0

RUN apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y && apt-get autoremove -y

# COPY php/conf/php-ini-overrides.ini  /usr/local/etc/php/conf.d/php-ini-overrides.ini

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ENV COMPOSER_ALLOW_SUPERUSER=1

WORKDIR /app

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

# add mhsendmail (sendmail is forced to use smtp)
RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.10.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail