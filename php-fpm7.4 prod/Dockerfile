FROM php:7.4-fpm-alpine

RUN apk update && apk upgrade
# Install dependencies
RUN apk add mariadb-client libpng-dev libssh-dev zip libzip-dev libxml2-dev jpegoptim optipng pngquant gifsicle unzip git libxslt-dev curl rabbitmq-c-dev icu-dev oniguruma-dev

# Install extensions
RUN apk add --no-cache $PHPIZE_DEPS \
   && pecl install redis amqp \
   && docker-php-ext-enable redis amqp

RUN docker-php-ext-install opcache pdo_mysql mysqli zip mbstring bcmath sockets xsl exif gd intl

WORKDIR /var/www

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]