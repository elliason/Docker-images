FROM node:18

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN apt-get update && apt-get upgrade -y

USER node

RUN curl -fsSL https://get.pnpm.io/install.sh | bash -

RUN npm install -g pnpm

WORKDIR /var/www/html