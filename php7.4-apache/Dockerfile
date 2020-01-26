FROM php:7.4-apache

ARG WEB_USER
ARG WEB_GROUP
ARG WEBSERVER_ROOT_DIR
ARG WEBSERVER_LOGS_DIR
ARG WEBSERVER_CONFIG_DIR

# Surpresses debconf complaints of trying to install apt packages interactively
# https://github.com/moby/moby/issues/4032#issuecomment-192327844
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get -y update --fix-missing --no-install-recommends
RUN apt-get -y upgrade

# install useful tools
RUN apt-get update
RUN apt-get install -y nano
RUN apt-get install -y dialog
RUN apt-get install -y apt-utils
RUN apt-get install -y build-essential
RUN apt-get install -y libfreetype6-dev
RUN apt-get install -y libjpeg62-turbo-dev
RUN apt-get install -y libmcrypt-dev
RUN apt-get install -y libpng-dev
RUN apt-get install -y curl
RUN apt-get install -y libcurl4
RUN apt-get install -y libcurl4-openssl-dev
RUN apt-get install -y zlib1g-dev
RUN apt-get install -y libicu-dev
RUN apt-get install -y libmemcached-dev
RUN apt-get install -y memcached
RUN apt-get install -y default-mysql-client
RUN apt-get install -y libmagickwand-dev
RUN apt-get install -y unzip
RUN apt-get install -y libzip-dev
RUN apt-get install -y zip
RUN apt-get install -y iputils-ping
RUN apt-get install -y net-tools
RUN apt-get install -y git
RUN apt-get install -y wget
RUN apt-get install -y vim
RUN apt-get install -y libonig-dev

# configure, install and enable php packages
RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg
RUN docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd
RUN docker-php-ext-install -j$(nproc) pdo
RUN docker-php-ext-install -j$(nproc) pdo_mysql

RUN docker-php-ext-configure mysqli --with-mysqli=mysqlnd
RUN docker-php-ext-install -j$(nproc) mysqli

RUN docker-php-ext-configure intl
RUN docker-php-ext-install -j$(nproc) intl

RUN docker-php-ext-configure zip
RUN docker-php-ext-install -j$(nproc) zip

RUN docker-php-ext-install curl
RUN docker-php-ext-install tokenizer
RUN docker-php-ext-install json
RUN docker-php-ext-install gettext

# install xdebug
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_autostart=0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.default_enable=0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_host=host.docker.internal" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_connect_back=0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.profiler_enable=0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_log=\"/tmp/xdebug.log\"" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# install imagick
RUN pecl install imagick
RUN docker-php-ext-enable imagick

# install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Enable apache modules
RUN apt-get update -y
RUN a2enmod rewrite
RUN a2enmod headers
RUN a2enmod expires

# set webserver root folder
RUN sed -ri -e 's!/var/www/html!${WEBSERVER_ROOT_DIR}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${WEBSERVER_ROOT_DIR}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# copy apache configuration files
COPY ./vhost.conf ${WEBSERVER_CONFIG_DIR}/sites-available/000-default.conf

# copy php configuration
# Use the default production configuration
# RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
# Use my own
COPY ./php.ini $PHP_INI_DIR/php.ini

WORKDIR ${WEBSERVER_ROOT_DIR}

RUN usermod -u 1000 ${WEB_USER} \
 && groupmod -g 1000 ${WEB_GROUP} \
 && chgrp -R ${WEB_GROUP} ${WEBSERVER_ROOT_DIR}
