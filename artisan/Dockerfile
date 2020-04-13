ARG PHP_VERSION
FROM php:${PHP_VERSION}

LABEL MAINTAINER Yamashita<r.yamashita@edge-tech.co.jp>

RUN apt-get -y update && \
    apt-get -y install libpng-dev libzip-dev
RUN docker-php-ext-install pdo_mysql gd zip

WORKDIR /laravel

ENTRYPOINT [ "php", "artisan" ]
CMD ["list"]
