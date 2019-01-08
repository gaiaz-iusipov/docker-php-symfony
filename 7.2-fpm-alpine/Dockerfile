FROM php:7.2-fpm-alpine

LABEL maintainer="Gaiaz Iusipov <g.iusipov@gmail.com>"

COPY --from=gaiaz/php-extensions:7.2-alpine \
    /apcu.so \
    /intl.so \
    /opcache.so \
    /usr/local/lib/php/extensions/no-debug-non-zts-20170718/

RUN set -xe \
    && docker-php-ext-enable \
        apcu \
        opcache \
    && apk add --quiet --no-cache \
        icu \
    && docker-php-ext-enable \
        intl

COPY config/core.ini \
    config/opcache.ini \
    config/realpath.ini \
    /usr/local/etc/php/conf.d/

RUN addgroup -g 1000 docker \
    && adduser -u 1000 -G docker -h /home/docker -s /bin/sh -D docker

WORKDIR /app
