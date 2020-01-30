FROM php:7.2-alpine

# phpize
RUN apk add --update --no-cache $PHPIZE_DEPS

# memcached
RUN \
  apk add --uodate --no-cache cyrus-sasl-dev libmemcached-dev zlib-dev \
  && pecl install memcached \
  && docker-php-ext-enable memcached

# gd
RUN \
  apk add --update --no-cache libjpeg-turbo-dev libpng-dev libwebp-dev \
  && docker-php-ext-install gd

# intl
RUN \
  apk add --update --no-cache icu-dev \
  && docker-php-ext-install intl

# mysqli
RUN docker-php-ext-install mysqli

# opcache
RUN docker-php-ext-enable opcache

# pdo
RUN docker-php-ext-install pdo_mysql

# zip
RUN \
  apk add --update --no-cache libzip-dev \
  && docker-php-ext-install zip

# supervisor
RUN apk add --update --no-cache supervisor
COPY ./supervisord.conf /etc/
COPY ./laravel-scheduler.conf /etc/supervisord/conf.d/
COPY ./laravel-worker.conf /etc/supervisord/conf.d/

ENTRYPOINT ["/usr/bin/supervisord", "--nodaemon", "--configuration",  "/etc/supervisord.conf"]
