FROM php:7.3-cli-alpine

LABEL maintainer="Gaiaz Iusipov <g.iusipov@gmail.com>"

COPY --from=gaiaz/php-extensions:7.3-alpine \
    /apcu.so \
    /intl.so \
    /opcache.so \
    /usr/local/lib/php/extensions/no-debug-non-zts-20180731/

RUN set -xe \
    && docker-php-ext-enable \
        apcu \
        opcache \
    && apk add --quiet --no-cache \
        icu \
    && docker-php-ext-enable \
        intl

RUN set -xe \
    && sed --in-place \
            "$PHP_INI_DIR/php.ini-production" \
            "$PHP_INI_DIR/php.ini-development" \
        --expression 's/^;\(opcache\.memory_consumption\).*/\1 = 256/' \
        --expression 's/^;\(opcache\.max_accelerated_files\).*/\1 = 20000/' \
        --expression '/^;realpath_cache_size.*/s/^;//' \
        --expression 's/^;\(realpath_cache_ttl\).*/\1 = 600/' \
    && sed --in-place \
           "$PHP_INI_DIR/php.ini-production" \
       --expression 's/^;\(opcache\.validate_timestamps\).*/\1 = 0/'

COPY --from=gaiaz/php-tools:7.3-alpine \
    /composer \
    /usr/local/bin/

RUN addgroup -g 1000 docker \
    && adduser -u 1000 -G docker -h /home/docker -s /bin/sh -D docker

RUN mkdir /app \
    && chown docker /app

WORKDIR /app
