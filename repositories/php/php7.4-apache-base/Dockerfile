FROM php:7.4-apache

## Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Dependencies
RUN apt-get update -y && apt-get install -y ssh libpng-dev libmagickwand-dev libjpeg-dev libmemcached-dev zlib1g-dev libzip-dev git unzip subversion ca-certificates libicu-dev libxml2-dev libmcrypt-dev
RUN apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/

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

# Config - enable apache modules
RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2enmod headers
RUN a2enmod expires

# http://blog.oddbit.com/post/2019-02-24-docker-build-learns-about-secr/
# This is necessary to prevent the "git clone" operation from failing
# with an "unknown host key" error.
RUN mkdir -m 700 /root/.ssh; \
  touch -m 600 /root/.ssh/known_hosts; \
  ssh-keyscan github.com > /root/.ssh/known_hosts