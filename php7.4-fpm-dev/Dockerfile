FROM php:7.4-fpm-alpine

RUN apk update && apk upgrade
# Install dependencies
RUN apk add mariadb-client libpng-dev postgresql-dev libssh-dev zip libzip-dev libxml2-dev jpegoptim optipng pngquant gifsicle unzip git libxslt-dev curl rabbitmq-c-dev icu-dev oniguruma-dev

# Install extensions
RUN apk add --no-cache $PHPIZE_DEPS \
   && pecl install redis amqp xdebug mongodb \
   && docker-php-ext-enable redis amqp xdebug mongodb

RUN docker-php-ext-install opcache pdo_mysql pdo_pgsql mysqli zip mbstring bcmath sockets xsl exif gd intl

WORKDIR /var/www

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]