# First Stage: Build
FROM php:8.3.8-fpm AS build

# Install system dependencies
RUN apt-get update && apt-get install -y  \
    curl \
    libzip-dev \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libfontconfig1 \
    libxrender1 \
    libxext6 \
    locales \
    zip \
    nginx \
    supervisor

# Install PHP extensions
RUN docker-php-ext-install gd pdo_mysql zip exif pcntl sockets opcache
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN pecl install excimer # for sentry

# Copy opcache config
COPY ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini

# Install Node.js
RUN apt-get install -y nodejs

# Install Bun
RUN curl -fsSL https://bun.sh/install | bash
ENV PATH="$PATH:/root/.bun/bin"
# Global bun installation
ENV PATH="$PATH:/root/.bun/install/global/node_modules/.bin"

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
