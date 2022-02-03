FROM php:8.1.2-fpm-alpine

RUN apk update --no-cache \
    && apk upgrade --no-cache \
    && apk add --no-cache build-base autoconf supervisor

RUN docker-php-ext-install pdo_mysql

RUN pecl install -o -f redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis

RUN apk del build-base autoconf

CMD ["supervisord", "-n", "-c", "/etc/supervisor/conf.d/supervisord.conf", "-e", "debug"]