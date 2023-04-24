FROM node:18-bullseye

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN npm install -g pnpm

RUN apt-get install iputils-ping -y

USER node

SHELL ["/bin/bash", "-c"]

WORKDIR /var/www/html