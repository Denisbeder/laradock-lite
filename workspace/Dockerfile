ARG PHP_VERSION

FROM php:${PHP_VERSION}-fpm

ENV NODE_VERSION=16

# Set Environment Variables
ENV DEBIAN_FRONTEND=noninteractive

# always run apt update when start and after add new source list, then clean up at end.
RUN set -eux; \
    apt-get update && \
    apt-get upgrade -y && \
    pecl channel-update pecl.php.net && \
    apt-get install -y --no-install-recommends \
    build-essential \
    apt-utils \
    gnupg2 \
    chrpath \
    wget \
    libbz2-dev \
    libssl-dev \
    libxft-dev \
    libmemcached-dev \
    libz-dev \
    libpq-dev \
    libjpeg-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libfreetype6 \
    libfreetype6-dev \
    libwebp-dev \
    libxpm-dev \
    libmcrypt-dev \
    libonig-dev \
    libfontconfig1 \
    libfontconfig1-dev

# install util packages
RUN apt-get install -y \
    libzip-dev zip unzip \
    git \
    vim \
    nano \
    tree \
    mariadb-client \
    postgresql-client

# install images optimizers
RUN apt-get install -y jpegoptim optipng pngquant gifsicle

# install extra PHP extenssions
RUN pecl install -o -f redis memcached xdebug && rm -rf /tmp/pear && \
    docker-php-ext-enable redis xdebug memcached && \
    docker-php-ext-configure gd --with-jpeg --with-webp --with-xpm --with-freetype && \
    docker-php-ext-install pdo_mysql exif opcache gd bz2

RUN rm /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# install PhantonJS to create Screenshots
RUN wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2 && \
    tar xvjf phantomjs-2.1.1-linux-x86_64.tar.bz2 -C /usr/local/share/ && \
    ln -sf /usr/local/share/phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/bin && \
    echo "export OPENSSL_CONF=/etc/ssl/" >> ~/.bashrc && . ~/.bashrc && \
    rm -f phantomjs-2.1.1-linux-x86_64.tar.bz2

# install NodeJS
RUN set -xe; \
    curl -sL https://deb.nodesource.com/setup_${NODE_VERSION}.x | bash - && \
    apt-get update && \
    apt-get install -y \
    nodejs

# install Yarn
RUN set -xe; \ 
    curl -o- -L https://yarnpkg.com/install.sh | bash

# Install composer
RUN php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

# Clean up
RUN apt-get clean && rm -rf /var/cache/apk/* /var/lib/apt/lists/* 

WORKDIR /var/www