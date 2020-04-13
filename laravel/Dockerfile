ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm

RUN apt-get -y update && \
    apt-get -y install sendmail libpng-dev libzip-dev
RUN docker-php-ext-install pdo_mysql gd zip

WORKDIR /laravel
