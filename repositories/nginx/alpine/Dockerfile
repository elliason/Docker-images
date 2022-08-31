FROM nginx:alpine

LABEL org.opencontainers.image.authors="info@eliasondrej.com"

RUN apk update && apk upgrade

# Add some packages
RUN apk add --no-cache bash \
    bash-completion \
    curl

# Add non-root user
RUN addgroup -g 1000 -S app \
    && adduser -u 1000 -D -S -G app app

# Copy the nginx configuration \
COPY ./etc/nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf

RUN mkdir /app
WORKDIR /app

# Add permissions for app user
RUN chown -R app:app /var/cache/nginx \
    && chown -R app:app /var/run \
    && chown -R app:app /var/log/nginx \
    && chown -R app:app /etc/nginx \
    && chown -R app:app /app \
    && chmod -R 775 /app

RUN touch /var/run/nginx.pid \
    && chown -R app:app /var/run/nginx.pid

# Expose port 8080
EXPOSE 8080

# Run the container as non-root user
USER app
