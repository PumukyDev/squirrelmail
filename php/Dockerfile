FROM php:7.3-fpm


COPY php.ini /usr/local/etc/php/php.ini

RUN mkdir -p /var/local/squirrelmail/data && \
    chown -R www-data:www-data /var/local/squirrelmail/data && \
    chmod -R 770 /var/local/squirrelmail/data

# Install required PHP extensions
RUN docker-php-ext-install pdo pdo_mysql


# Update package manager and install useful tools
RUN apt-get update && apt-get -y install apt-utils nano wget dialog vim


# Install important libraries
RUN echo "Install important libraries"
RUN apt-get -y install --fix-missing \
    apt-utils \
    build-essential \
    git \
    curl \
    libcurl4 \
    libcurl4-openssl-dev \
    zlib1g-dev \
    libzip-dev \
    zip \
    libbz2-dev \
    locales \
    libmcrypt-dev \
    libicu-dev \
    libonig-dev \
    libxml2-dev


# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*


# Add any additional configurations or adjustments as needed


# Set the working directory
WORKDIR /var/www/html


# Expose the port
EXPOSE 9000

# Set permissions for the web root
RUN chown -R www-data:www-data /var/www/html && chmod -R 755 /var/www/html


# Define the entry point
CMD ["php-fpm"]