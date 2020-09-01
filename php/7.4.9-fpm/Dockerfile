FROM php:7.4.9-fpm-alpine
MAINTAINER billypon

ENV COMPOSER_VERSION 1.10.10

RUN apk add --no-cache \
        libintl icu-libs libmcrypt libzip libbz2 libpng libjpeg-turbo libwebp freetype \
        gettext-dev icu-dev libmcrypt-dev libzip-dev zlib-dev bzip2-dev \
        libpng-dev libjpeg-turbo-dev libwebp-dev freetype-dev \
		openssl \
		openldap openldap-dev \

    && docker-php-ext-configure gd --with-jpeg --with-webp --with-freetype \
    && docker-php-ext-configure ldap \
    && pecl bundle -d /usr/src/php/ext mcrypt \
    && pecl bundle -d /usr/src/php/ext redis \
    && docker-php-ext-install bcmath bz2 calendar exif gd gettext intl mcrypt mysqli pdo_mysql pcntl sockets zip redis ldap \

    && apk del \
        gettext-dev icu-dev libmcrypt-dev libzip-dev zlib-dev bzip2-dev \
        libpng-dev libjpeg-turbo-dev libwebp-dev freetype-dev \
		openldap-dev \
    
    && rm -rf /tmp/pear/cache \

	&& wget -O /usr/local/bin/composer https://getcomposer.org/download/$COMPOSER_VERSION/composer.phar && chmod +x /usr/local/bin/composer
