FROM node:18-alpine3.17

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN apk update && apk upgrade

RUN apk add --no-cache bash \
    bash-completion \
    curl

RUN apk add --no-cache libjpeg-turbo \
    libjpeg-turbo-dev \
    libpng \
    libpng-dev \
    libwebp \
    libwebp-dev \
    libxpm \
    libxpm-dev \
    build-base \
    libc6-compat \
    ffmpeg

RUN npm install -g pnpm

USER node

SHELL ["/bin/bash", "-c"]

WORKDIR /var/www/html