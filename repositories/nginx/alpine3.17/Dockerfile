FROM nginx:stable-alpine3.17

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN apk update && apk upgrade

# Add some packages
RUN apk add --no-cache bash \
    bash-completion \
    curl

# Add non-root user with the same UID and GID as your current user
ARG UID=1000
ARG GID=1000

# Add non-root user
RUN addgroup -g ${GID} -S server \
    && adduser -u ${UID} -D -S -G server server

# Add permissions for app user
RUN chown -R server:server /var/cache/nginx \
    && chown -R server:server /var/run \
    && chown -R server:server /var/log/nginx \
    && chown -R server:server /etc/nginx

RUN touch /var/run/nginx.pid \
    && chown -R server:server /var/run/nginx.pid

# Expose port 8080
EXPOSE 8080

# Run the container as non-root user
USER server
WORKDIR /var/www/html