FROM php:7.3-apache
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libyaml-dev \
        libzip-dev \
        libbz2-dev \
    && docker-php-ext-install -j$(nproc) iconv mysqli pdo pdo_mysql \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && pecl install yaml \
    && docker-php-ext-enable yaml \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-install -j$(nproc) bz2 \
    && docker-php-ext-enable bz2

RUN a2enmod rewrite headers

COPY php.ini /usr/local/etc/php/conf.d/php.ini

COPY vhost.conf /etc/apache2/sites-available/000-default.conf

RUN touch /var/www/error.log /var/www/access.log
RUN chown www-data:www-data /var/www/error.log /var/www/access.log


