FROM php:7.2-fpm-alpine

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

RUN apk add --no-cache bash autoconf build-base \
    && apk add --no-cache bash wget libpng-dev libmcrypt-dev libstdc++ libevent-dev pcre-dev \
    && docker-php-ext-install gd mysqli pdo_mysql bcmath opcache pcntl sockets zip \
    && pecl install oauth \
    && pecl install redis \
    && pecl install mongodb \
    && pecl install swoole \
    && pecl install channel://pecl.php.net/mcrypt-1.0.1 \

    && apk add --no-cache freetype-dev jpeg-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \

    && apk add --no-cache libssh2-dev \
    && wget http://pecl.php.net/get/ssh2-1.1.2.tgz \
    && tar zxvf ssh2-1.1.2.tgz && cd ssh2-1.1.2 && phpize && ./configure --with-ssh2 && make \
    && mv modules/ssh2.so /usr/local/lib/php/extensions/no-debug-non-zts-20170718 \
    && cd .. && rm -rf ssh2-1.1.2* \

    && apk del build-base autoconf

RUN echo "export TERM=xterm" >> /root/.bashrc \
    && rm -rf /usr/local/etc/php-fpm.conf \
    && mkdir /php \
    && ln -s /php/php.ini /usr/local/etc/php/php.ini \
    && ln -s /php/php-fpm.conf /usr/local/etc/php-fpm.conf

USER root

RUN apk add --no-cache git

WORKDIR /www

CMD php-fpm
