FROM php:7.3-fpm
 
# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    mariadb-client \
    libpq-dev \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    librabbitmq-dev \
    libssh-dev \
    zip \
    libzip-dev \
    libxml2-dev \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    cron \
    libxslt-dev \
    curl\
    libcurl4-openssl-dev\
    pkg-config\
    libssl-dev

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install extensions
RUN docker-php-source extract && \
    pecl install xdebug redis mongodb amqp && \
    docker-php-ext-enable xdebug redis mongodb amqp  && \
    docker-php-source delete

RUN docker-php-ext-install opcache pdo_mysql pdo_pgsql xml intl zip mbstring bcmath sockets xsl exif gd

WORKDIR /var/www

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]
