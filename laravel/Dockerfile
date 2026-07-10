# First Stage: Build
FROM php:8.3.8-fpm AS build

# Install system dependencies
RUN apt-get update && apt-get install -y \
    curl \
    libzip-dev \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libfontconfig1 \
    libicu-dev \
    libxrender1 \
    libxext6 \
    locales \
    zip \
    nginx \
    supervisor \
    # Install PHP extensions
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-configure intl \
    && docker-php-ext-install gd pdo_mysql zip exif pcntl sockets opcache intl \
    && pecl install excimer # for sentry

# Install Node.js 22 
RUN curl -fsSL https://deb.nodesource.com/setup_22.x | bash - \
    && apt-get install -y nodejs

# Copy opcache config
COPY ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini
COPY ./php.ini /usr/local/etc/php/conf.d/php.ini

# Install Bun
RUN curl -fsSL https://bun.sh/install | bash
ENV PATH="$PATH:/root/.bun/bin:/root/.bun/install/global/node_modules/.bin"

# Get latest Composer
COPY --from=composer:2.2.25 /usr/bin/composer /usr/bin/composer