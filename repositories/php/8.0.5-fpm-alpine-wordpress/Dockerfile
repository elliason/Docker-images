FROM php:8.0.5-fpm-alpine

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN apk update && apk upgrade

# Add some packages
RUN apk add --no-cache bash \
    bash-completion \
    curl

# Install MySQLi
RUN docker-php-ext-install mysqli

# Add more packages for wordpress
RUN apk add --no-cache ca-certificates \
    autoconf \
    icu-dev \
    g++ \
    gcc \
    imagemagick \
    imagemagick-dev \
    imagemagick-c++ \
    libzip-dev \
    libtool \
    make \
    openssl \
    php8-exif \
    php-intl \
    php8-mysqli \
    php8-pecl-imagick \
    php8-zip \
    tar \
    xz \
    zip \
    zlib-dev \
    pcre-dev

RUN docker-php-ext-install bcmath exif intl zip
RUN pecl install imagick && docker-php-ext-enable imagick
RUN docker-php-ext-enable sodium
#RUN apk del autoconf bzip2-dev gcc g++ libtool icu-dev make musl-dev imagemagick-dev imagemagick-c++ libzip-dev perl xz-dev zlib-dev zstd-dev
#RUN rm -f /tmp/pear/download/imagick*

# Add WP CLI
RUN curl -o /usr/local/bin/wp https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && chmod +x /usr/local/bin/wp

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