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
    excimer \
    locales \
    zip \
    unzip \
    nginx \
    supervisor

# Install PHP extensions
RUN docker-php-ext-install gd pdo_mysql zip exif pcntl sockets
RUN docker-php-ext-configure gd --with-freetype --with-jpeg

# Install Node.js and Yarn
RUN curl -sL https://deb.nodesource.com/setup_20.x | bash -
RUN apt-get install -y nodejs

# Install PNPM
RUN curl -fsSL https://get.pnpm.io/install.sh | sh -

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer