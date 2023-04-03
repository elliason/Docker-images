FROM php:8.2.4-fpm-bullseye

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN apt-get update && apt-get upgrade -y

# Install dependencies
RUN apt-get install -y \
    git \
    unzip \
    wget \
    ssh \
    libpng-dev \
    libmagickwand-dev \
    libjpeg-dev \
    libmemcached-dev \
    zlib1g-dev \
    libzip-dev \
    ca-certificates \
    libicu-dev \
    libxml2-dev \
    libmcrypt-dev

RUN apt-get autoremove -y && apt-get clean

# Install Composer
RUN wget -O composer-setup.php https://getcomposer.org/installer \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && rm composer-setup.php

# PHP Extensions - PECL
RUN pecl install imagick memcached mcrypt && docker-php-ext-enable imagick memcached mcrypt

# PHP Extensions - docker-php-ext-install
RUN docker-php-ext-install zip gd mysqli exif pdo pdo_mysql opcache intl soap

# PHP Extensions - docker-php-ext-configure
RUN docker-php-ext-configure intl

# Xdebug
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

# PHP Tools
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && chmod +x wp-cli.phar && mv wp-cli.phar /usr/local/bin/wp

ARG UID=1000
ARG GID=1000

# Add a user php with the same UID and GID as your current user
RUN groupadd -g ${GID} php && \
    useradd -u ${UID} -g php -m php

# Set the user for the following RUN, CMD and ENTRYPOINT instructions
USER php
WORKDIR /var/www/html