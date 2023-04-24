FROM node:18

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN apt-get update && apt-get upgrade -y

RUN apt install graphviz -y

RUN apt-get install iputils-ping -y

RUN npm install -g pnpm

USER node

WORKDIR /var/www/html