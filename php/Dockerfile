FROM php:7.4.11-fpm
COPY config/php.ini /usr/local/etc/php
COPY ./opt/composer  /usr/local/bin/composer
COPY ./opt/amqp-1.10.2.tgz  /opt/amqp-1.10.2.tgz
COPY ./opt/phpredis-5.3.0.tar.gz  /opt/phpredis-5.3.0.tar.gz
COPY ./opt/swoole-src-4.5.2.tar.gz  /opt/swoole-src-4.5.2.tar.gz
RUN apt-get update \
    && apt-get  install -y apt-utils  libpng12*-dev vim  libmcrypt-dev libfreetype6-dev \
    libpng-dev libjpeg-dev  libjpeg62-turbo-dev  wget libmcrypt-dev \
    docker-php-ext-install  mcrypt
    && docker-php-ext-install pdo_mysql mysqli pcntl gd mbstring   \  
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/  --with-png-dir=/usr/include --enable-gd-native-ttf 
RUN  mkdir -p /usr/src/php/ext  &&  chmod +x  /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ \
    && tar -zxvf  /opt/phpredis-5.3.0.tar.gz  \ 
    && mv /opt/phpredis-5.3.0  /usr/src/php/ext/redis \
    && docker-php-ext-install redis \
    && mkdir -p /usr/src/php/ext \
    && tar -zxvf /opt/amqp-1.10.2.tgz \
    && mv /opt/amqp-1.10.2  /usr/src/php/ext/amqp \
    && apt-get install -y librabbitmq-dev \
    && docker-php-ext-install amqp \
    && mkdir -p /usr/src/php/ext \
    && tar -zxvf /opt/swoole-src-4.5.2.tar.gz \
    && mv swoole-src-4.5.2  /usr/src/php/ext/swoole && docker-php-ext-install swoole