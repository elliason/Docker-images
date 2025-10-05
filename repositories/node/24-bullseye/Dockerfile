FROM node:24-bullseye

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN npm install -g pnpm

RUN npm install -g tsx

USER node

SHELL ["/bin/bash", "-c"]

WORKDIR /var/www/html