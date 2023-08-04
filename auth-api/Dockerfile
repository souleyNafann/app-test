# Use the official PHP image as the base image
FROM php:8.1-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libjpeg-dev \
    libpq-dev \
    libfreetype6-dev \
    zip \
    unzip

# Install PHP extensions, we using postgresql
RUN docker-php-ext-install pdo pdo_pgsql pgsql


# Set the working directory in the container
WORKDIR /var/www

# Copy the Laravel project files into the container
COPY . /var/www

# Install Composer (if not already installed)
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install project dependencies using Composer
RUN composer install

# Set proper permissions for Laravel storage and cache folders
RUN chown -R www-data:www-data /var/www/storage/logs/
RUN chmod -R 777 storage




# Expose port 9000 for PHP-FPM
EXPOSE 9000

# Start PHP-FPM server
CMD ["php-fpm"]

