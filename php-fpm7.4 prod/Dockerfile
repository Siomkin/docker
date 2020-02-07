FROM php:7.4-fpm
 
# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    mariadb-client \
    libpng-dev \
    libonig-dev \
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
    pecl install redis amqp && \
    docker-php-ext-enable redis amqp  && \
    docker-php-source delete

RUN docker-php-ext-install opcache pdo_mysql xml intl zip mbstring bcmath sockets xsl exif gd

WORKDIR /var/www

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]
