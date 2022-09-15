FROM node:17-alpine3.15

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN apk update && apk upgrade

RUN apk add --no-cache bash \
    bash-completion \
    curl

RUN mkdir /app \
    && chown -R node:node /app \
    && chmod -R 775 /app

WORKDIR /app

USER node