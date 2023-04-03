FROM php:8.2.4-fpm-bullseye

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN apt-get update && apt-get upgrade -y

# Install dependencies
RUN apt-get install -y \
    git \
    unzip \
    wget

# Install Composer
RUN wget -O composer-setup.php https://getcomposer.org/installer \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && rm composer-setup.php    

ARG UID=1000
ARG GID=1000

# Add a user php with the same UID and GID as your current user
RUN groupadd -g ${GID} php && \
    useradd -u ${UID} -g php -m php

# Set the user for the following RUN, CMD and ENTRYPOINT instructions
USER php
WORKDIR /var/www/html