FROM php:7.3-fpm

USER root

RUN apt-get update

# --- Install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# --- Install and configure supervisord
RUN apt-get -y install supervisor
COPY ./etc/supervisor/conf.d/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# --- Install dependencies
RUN apt-get install -y zip \
                       git \
                       vim \
                       curl \
                       mariadb-client \
                       libpng-dev \
                       libicu-dev \
                       libxml2-dev \
                       libxslt-dev \
                       libzip-dev \
                       libfreetype6-dev \
                       libjpeg62-turbo-dev \
                       libmcrypt-dev

RUN docker-php-ext-configure gd --with-jpeg-dir=/usr/include/ --with-freetype-dir=/usr/include
RUN docker-php-ext-install bcmath \
                           gd \
                           intl \
                           pdo_mysql \
                           soap \
                           xsl \
                           zip \
                           sockets

# --- Setup user
RUN groupadd --gid 2222 magento
RUN useradd magento --uid 2222 -m -g magento
RUN echo "magento:magento" | chpasswd

RUN sed -i 's/www-data/magento/g' /usr/local/etc/php-fpm.d/www.conf
RUN sed -i 's/www-data/magento/g' /usr/local/etc/php-fpm.d/www.conf.default

COPY ./usr/local/etc/php/php.ini /usr/local/etc/php/php.ini

WORKDIR /var/www/magento23os

EXPOSE 9000

CMD [ "supervisord", "-n" ]