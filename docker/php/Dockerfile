FROM drupal:8-fpm

RUN apt-get update && apt-get install \
    && pecl install apcu \
    && docker-php-ext-enable apcu