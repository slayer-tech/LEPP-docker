FROM php:8-fpm
WORKDIR "/application"
ENV COMPOSER_ALLOW_SUPERUSER=1

ARG DEBIAN_FRONTEND=noninteractive

RUN apt update && apt-get update && apt-get install -y \
        curl \
        wget \
        git \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
    libpq-dev\
	libpng-dev \
	libonig-dev \
	libzip-dev \
	libmcrypt-dev \
        && docker-php-ext-install -j$(nproc) iconv mbstring mysqli pdo_mysql zip \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
        && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) pdo_pgsql

# Установим pdo для postgresql
RUN docker-php-ext-install pdo pdo_pgsql

# Install composer 
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer