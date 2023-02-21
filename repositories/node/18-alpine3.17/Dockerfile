FROM node:18-alpine3.17

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN apk update && apk upgrade

RUN apk add --no-cache bash \
    bash-completion \
    curl

RUN mkdir /app \
    && chown -R node:node /app \
    && chmod -R 775 /app

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

USER node

RUN wget -qO- https://get.pnpm.io/install.sh | ENV="~/.bashrc" SHELL="$(which bash)" bash -

WORKDIR /app