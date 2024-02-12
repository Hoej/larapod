FROM php:8.3-fpm-alpine3.19

WORKDIR /var/www

ENV PHP_OPCACHE_VALIDATE_TIMESTAMPS="0" \
    PHP_OPCACHE_MAX_ACCELERATED_FILES="10957" \
    PHP_OPCACHE_MEMORY_CONSUMPTION="256" \
    PHP_OPCACHE_MAX_WASTED_PERCENTAGE="10"

# Install required packages
RUN apk add --update --no-cache \
    nano \
    nginx \
    supervisor \
    autoconf \
    build-base \
    libzip-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    linux-headers

RUN pecl install redis xdebug excimer
RUN docker-php-ext-install pdo_mysql opcache pcntl exif
RUN docker-php-ext-enable redis xdebug excimer

# Install composer
ADD scripts/install-composer.sh /var/www/
RUN /var/www/install-composer.sh

COPY conf/supervisord.conf /etc/supervisor/conf.d/
COPY conf/nginx.conf /etc/nginx/
COPY conf/php.ini /usr/local/etc/php/php.ini
COPY conf/opcache.ini /usr/local/etc/php/conf.d/
COPY conf/xdebug.ini /usr/local/etc/php/conf.d/
COPY conf/php-fpm.conf /usr/local/etc/php-fpm.d/zz-docker.conf

RUN mkdir -p "/var/run/php-fpm"

# Setup 1min cron jobs
COPY scripts/artisan-schedule-run /etc/periodic/1min/
RUN echo "*       *       *       *       *       run-parts /etc/periodic/1min" >> /etc/crontabs/root

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
