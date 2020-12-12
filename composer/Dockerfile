ARG PHP_VERSION
FROM php:${PHP_VERSION}

LABEL MAINTAINER Yamashita<darum@yamas.xyz>

RUN apt-get update -y
RUN apt-get install -y --fix-missing git unzip libpng-dev libzip-dev

RUN docker-php-ext-install gd zip pdo_mysql

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN composer self-update
RUN echo 'precedence ::ffff:0:0/96 100' >> /etc/gai.conf
RUN composer config -g repos.packagist composer https://packagist.jp

ENV HOME /composer
WORKDIR /laravel

ENTRYPOINT [ "composer" ]
CMD ["--help"]
