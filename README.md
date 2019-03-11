# docker-php-symfony

[![GitHub](https://img.shields.io/github/license/gaiaz-iusipov/docker-php-symfony.svg)](https://github.com/gaiaz-iusipov/docker-php-symfony#license)
[![Docker Pulls](https://img.shields.io/docker/pulls/gaiaz/php-symfony.svg)](https://hub.docker.com/r/gaiaz/php-symfony/)

:whale: [Alpine](https://alpinelinux.org/) Linux based [Docker](https://www.docker.com/) Image for [Symfony](https://symfony.com/) applications.

## Extensions

- [APCu](https://pecl.php.net/package/APCu)
- Intl
- OPcache

## Tools

- [Composer](https://getcomposer.org/) - Dependency Manager for PHP

## Usage

```dockerfile
FROM gaiaz/php-symfony:7.3-fpm-alpine

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" \
    && rm "$PHP_INI_DIR/php.ini-development

# or development configuration
# RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini" \
#     && rm "$PHP_INI_DIR/php.ini-production"
```

## License

[MIT](http://opensource.org/licenses/MIT) © [Gaiaz Iusipov](https://github.com/gaiaz-iusipov)
