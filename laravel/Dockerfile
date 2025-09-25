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
    libicu-dev \
    libxrender1 \
    libxext6 \
    locales \
    zip \
    nginx \
    supervisor \
    # Install PHP extensions
    && docker-php-ext-install gd pdo_mysql zip exif pcntl sockets opcache intl \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-configure intl \
    && pecl install excimer # for sentry

# Install nodejs
RUN curl -o- https://fnm.vercel.app/install | bash
RUN fnm install 22

# Copy opcache config
COPY ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini
COPY ./php.ini /usr/local/etc/php/conf.d/php.ini

# Install Bun
RUN curl -fsSL https://bun.sh/install | bash
ENV PATH="$PATH:/root/.bun/bin:/root/.bun/install/global/node_modules/.bin"

# Get latest Composer
COPY --from=composer:2.2.25 /usr/bin/composer /usr/bin/composer
