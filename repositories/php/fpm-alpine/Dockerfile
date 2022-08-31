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

RUN mkdir /app
WORKDIR /app

# Add non-root user
RUN addgroup -g 1000 -S app \
    && adduser -u 1000 -D -S -G app app

RUN chown -R app:app /app \
    && chmod -R 775 /app

# Run the container as non-root user
USER app