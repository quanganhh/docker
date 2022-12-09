FROM php:7.4-fpm

# Set working directory
WORKDIR /var/www

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    nodejs \
    npm \
    curl \
    libzip-dev \
    libicu-dev

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install extensions
# gd need config os libs like jpeg, png path before install
RUN docker-php-ext-install pdo_mysql zip exif pcntl gd intl

# XDEBUG
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer global require "squizlabs/php_codesniffer=*"

# Add user for laravel application
# Need pass userid based on each pc by setting on env
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

# Change current user to www
USER www

# Expose port 9000 and start php-fpm server
EXPOSE 9000

# Need a entrypoint here to run app migration, create app key and anything else

CMD ["php-fpm"]
