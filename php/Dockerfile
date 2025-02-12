FROM php:7.3-fpm

RUN apt-get update && apt-get install -y \
    locales \
    nano \
    wget \
    git \
    libzip-dev \
    zip

COPY php.ini /usr/local/etc/php/php.ini

RUN mkdir -p /var/local/squirrelmail/data /var/local/squirrelmail/attach && \
    chown -R www-data:www-data /var/local/squirrelmail && \
    chmod -R 777 /var/local/squirrelmail

WORKDIR /var/www/html

CMD ["php-fpm"]