FROM php:8.3.13-fpm

ARG UID=1000
ARG GID=1000

WORKDIR /var/www

RUN apt-get update \
    && apt-get install -y build-essential zlib1g-dev g++ git libicu-dev zip libzip-dev libpng-dev libcurl4-gnutls-dev \
    && docker-php-ext-install intl opcache pdo pdo_mysql gd mysqli curl \
    # && pecl install xdebug \
    # && docker-php-ext-enable xdebug \
    # xdebug required php 8+
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && pecl install zip \
    && docker-php-ext-enable zip \
    && apt-get install -y procps \
    && rm -rf /var/lib/apt/lists/* \
    && groupmod -g "${GID}" www-data && usermod -u "${UID}" -g "${GID}" www-data \
    && chown www-data:www-data -R /var/www

COPY /config/php/uploads.ini /usr/local/etc/php/conf.d/uploads.ini

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

USER www-data