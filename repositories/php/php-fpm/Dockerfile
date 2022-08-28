FROM php:fpm-alpine

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN apk update && apk upgrade

# Add some packages
RUN apk add --no-cache bash \
    bash-completion \
    curl

# Install MySQLi
RUN docker-php-ext-install mysqli

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer