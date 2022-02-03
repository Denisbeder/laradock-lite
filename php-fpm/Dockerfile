FROM php:8.1.2-fpm-alpine

# these PHP Modules have been installed already
#Core
#ctype
#curl
#date
#dom
#fileinfo
#filter
#ftp
#hash
#iconv
#json
#libxml
#mbstring
#mysqlnd
#openssl
#pcre
#PDO
#pdo_sqlite
#Phar
#posix
#readline
#Reflection
#session
#SimpleXML
#SPL
#sqlite3
#standard
#tokenizer
#xml
#xmlreader
#xmlwriter
#zlib

# install php extensions by docker-php-ext-install https://github.com/docker-library/php/issues/279

RUN apk update --no-cache \
    && apk upgrade --no-cache \
    && apk add --no-cache build-base autoconf
    
RUN docker-php-ext-install pdo_mysql

RUN pecl install -o -f redis xdebug \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis xdebug

RUN apk del build-base autoconf

RUN rm /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

WORKDIR /var/www

EXPOSE 9000

CMD ["php-fpm"]
