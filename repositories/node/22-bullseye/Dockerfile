FROM node:22-bullseye

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN npm install -g pnpm

USER node

SHELL ["/bin/bash", "-c"]

WORKDIR /var/www/html