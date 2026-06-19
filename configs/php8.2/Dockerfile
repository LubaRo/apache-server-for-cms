FROM php:8.2-apache

RUN set -xe; \
    apt-get update && apt-get install -y --no-install-recommends \
        $PHPIZE_DEPS;

RUN pecl install xdebug && docker-php-ext-enable xdebug
RUN docker-php-ext-install mysqli pdo pdo_mysql && docker-php-ext-enable mysqli;

# ----- zip -----
RUN apt-get update && apt-get install -y \
    libzip-dev \
    zip \
    unzip \
    git \
    && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-configure zip \
    && docker-php-ext-install zip

# ----- gd -----
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

# ----- Imagick -----
RUN apt-get update && apt-get install -y --no-install-recommends \
    libmagickwand-dev \
    && rm -rf /var/lib/apt/lists/*
RUN pecl install imagick \
    && docker-php-ext-enable imagick

RUN a2enmod rewrite;

# install the ssl-cert package which will create a "snakeoil" keypair
RUN apt-get update \
 && apt-get install -y ssl-cert \
 && rm -r /var/lib/apt/lists/*

# enable ssl module and enable the default-ssl site
RUN a2enmod ssl \
 && a2ensite default-ssl

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

