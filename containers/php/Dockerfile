FROM php:7.2-fpm-alpine

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

# composer
RUN curl -sS https://getcomposer.org/installer | php; mv composer.phar /usr/local/bin/composer
RUN composer global require phpunit/phpunit

WORKDIR /var/www/

# cron
RUN (crontab -l; echo "* * * * * root cd /var/www/ && php artisan schedule:run >> /dev/null 2>&1") | crontab -
RUN crond -l 1
