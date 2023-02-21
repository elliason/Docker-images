FROM node:18

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN apk update && apk upgrade

RUN mkdir /app \
    && chown -R node:node /app \
    && chmod -R 775 /app

USER node

RUN curl -fsSL https://get.pnpm.io/install.sh | sh -

WORKDIR /app