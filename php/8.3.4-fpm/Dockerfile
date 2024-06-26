FROM php:8.3.4-fpm-alpine
MAINTAINER billypon

ENV COMPOSER_VERSION 2.7.7

RUN apk add --no-cache \
        libintl icu-libs libmcrypt libzip libbz2 libpng libjpeg-turbo libwebp freetype \
        gettext-dev icu-dev libmcrypt-dev libzip-dev zlib-dev bzip2-dev \
        libpng-dev libjpeg-turbo-dev libwebp-dev freetype-dev \
        openssl \
        openldap openldap-dev \
        libgmpxx gmp-dev \
        imagemagick imagemagick-libs libgomp imagemagick-dev \
        linux-headers \

    && docker-php-ext-configure gd --with-jpeg --with-webp --with-freetype \
    && docker-php-ext-configure ldap \
    && pecl bundle -d /usr/src/php/ext apcu \
    && pecl bundle -d /usr/src/php/ext mcrypt \
    && pecl bundle -d /usr/src/php/ext redis \
    && pecl bundle -d /usr/src/php/ext imagick \
    && docker-php-ext-install bcmath bz2 calendar exif gd gettext intl mcrypt mysqli pdo_mysql pcntl sockets zip redis apcu opcache gmp imagick ldap \

    && apk del \
        gettext-dev icu-dev libmcrypt-dev libzip-dev zlib-dev bzip2-dev \
        libpng-dev libjpeg-turbo-dev libwebp-dev freetype-dev \
        openldap-dev \
        gmp-dev \
        imagemagick-dev \
        linux-headers \

    && rm -rf /tmp/pear/cache \

    && wget -O /usr/local/bin/composer https://getcomposer.org/download/$COMPOSER_VERSION/composer.phar && chmod +x /usr/local/bin/composer
