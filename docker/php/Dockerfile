FROM php:8.3-cli-alpine

# Arguments defined in docker-compose.yml
ARG user
ARG uid

# Install system dependencies
RUN apk add --no-cache \
    git \
    curl \
    libpng-dev \
    oniguruma-dev \
    libxml2-dev \
    zip \
    unzip \
    libzip-dev \
    nodejs \
    npm \
    ${PHPIZE_DEPS}

# Install PHP extensions
RUN docker-php-ext-install zip pdo_mysql mbstring exif pcntl bcmath gd

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Create system user to run Composer and Artisan Commands
RUN adduser -u $uid -h /home/$user -s /bin/sh -D $user \
    && addgroup $user www-data \
    && mkdir -p /home/$user/.composer \
    && chown -R $user:$user /home/$user

# Set working directory
WORKDIR /var/www

USER $user
