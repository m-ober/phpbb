FROM php:7.4-fpm

RUN pecl install xdebug; \
    docker-php-ext-enable xdebug; \
    echo "error_reporting=E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "display_startup_errors=On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "display_errors=On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.mode=develop,debug" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.client_port=9001" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.client_host=127.0.0.1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.start_with_request=trigger" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.force_display_errors=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini;

RUN echo "catch_workers_output = yes" >> /usr/local/etc/php-fpm.conf && \
    echo "php_admin_value[log_errors_max_len] = 0" >> /usr/local/etc/php-fpm.conf

RUN apt-get update -yqq && \
    apt-get install -yqq --no-install-recommends \
    locales-all libcurl4-gnutls-dev libpq-dev libmagickwand-dev unzip libzip-dev libjpeg-dev libfreetype6-dev && \
    docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install pgsql pdo_pgsql intl gd zip bz2 && \
    apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

WORKDIR /var/www/phpbb/

RUN mkdir -p /var/www/phpbb/cache && \
    chown www-data:www-data /var/www/phpbb/cache

VOLUME ["/var/www/phpbb/cache"]
