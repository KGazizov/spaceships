FROM php:8.1-fpm-alpine

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

COPY ./.docker/php-fpm/50-custom.ini /usr/local/etc/php/conf.d/50-custom.ini

WORKDIR /app/spaceships

RUN apk add --no-cache shadow && \
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    chmod +x /usr/local/bin/install-php-extensions && sync && \
    install-php-extensions bcmath gd imagick mysqli pdo_mysql redis memcached zip

RUN addgroup -g 1000 node \
    && adduser -u 1000 -G node -s /bin/sh -D node

USER 1000:1000

EXPOSE 9000
