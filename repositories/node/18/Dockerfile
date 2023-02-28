FROM node:18

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN apt-get update && apt-get upgrade -y

USER node

RUN "npm install -g pnpm"

RUN npm install -g pnpm

WORKDIR /var/www/html