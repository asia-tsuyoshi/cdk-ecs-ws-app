FROM php:8.2.11-fpm-bookworm

ENV TZ=Asia/Tokyo \
    COMPOSER_ALLOW_SUPERUSER=1 \
    COMPOSER_HOME=/composer

COPY --from=composer:2.6.5 /usr/bin/composer /usr/bin/composer

RUN apt-get update && \
    apt-get -y install unzip libzip-dev busybox-static && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    docker-php-ext-install pdo_mysql zip && \
    composer config -g process-timeout 3600 && \
    ln -sf /proc/1/fd/1 /var/log/cron.log

# readonlyRootFilesystem=true時に必要
VOLUME /var/laravel/storage
VOLUME /var/run

COPY ./docker/laravel/php.ini /usr/local/etc/php/php.ini
COPY ./docker/laravel/cron /var/spool/cron/crontabs/root

COPY ./laravel /var/laravel

WORKDIR /var/laravel

RUN composer install

CMD ["busybox", "crond", "-f"]