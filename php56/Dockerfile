FROM php:5.6-fpm-alpine

RUN apk add bash autoconf build-base \
    && apk add --no-cache bash wget libpng-dev libmcrypt-dev libstdc++ libevent-dev openssl-dev libzip-dev \
    && docker-php-ext-install gd mysql mysqli pdo_mysql bcmath opcache pcntl \

    && apk add freetype-dev jpeg-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \

    && pecl install channel://pecl.php.net/zip-1.15.5 \

    && apk del build-base autoconf

RUN echo "export TERM=xterm" >> /root/.bashrc \
    && rm -rf /usr/local/etc/php-fpm.conf \
    && mkdir /php \
    && ln -s /php/php.ini /usr/local/etc/php/php.ini \
    && ln -s /php/php-fpm.conf /usr/local/etc/php-fpm.conf


WORKDIR /www

CMD php-fpm
