FROM php:fpm-alpine
MAINTAINER billypon

ADD localtime /etc/localtime

RUN apk add --no-cache \
        libintl icu-libs libmcrypt libbz2 libpng libjpeg-turbo libwebp freetype \
        gettext-dev icu-dev libmcrypt-dev zlib-dev bzip2-dev \
        libpng-dev libjpeg-turbo-dev libwebp-dev freetype-dev \

    && docker-php-ext-configure gd --with-jpeg-dir=/usr/include --with-webp-dir=/usr/include --with-freetype-dir=usr/include \
    && pecl bundle -d /usr/src/php/ext redis \
    && docker-php-ext-install bcmath bz2 calendar exif gd gettext intl mcrypt mysqli pcntl sockets zip redis \

    && apk del \
        gettext-dev icu-dev libmcrypt-dev zlib-dev bzip2-dev \
        libpng-dev libjpeg-turbo-dev libwebp-dev freetype-dev \
    
    && rm -rf /tmp/pear/cache
