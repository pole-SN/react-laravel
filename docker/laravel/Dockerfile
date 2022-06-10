FROM php:8.1-rc-fpm-alpine

ENV TZ=Asia/Tokyo \
  LANG=ja_JP.UTF-8 \
  LANGUAGE=ja_JP:ja \
  LC_ALL=ja_JP.UTF-8 \
  COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

COPY --from=composer:2.3 /usr/bin/composer /usr/bin/composer

COPY ./app-laravel-backend /app/laravel
WORKDIR /app/laravel

RUN apk upgrade
RUN apk update
RUN apk --no-cache add git
RUN apk --no-cache add vim

RUN docker-php-ext-install pdo_mysql

RUN composer install -q -n --no-ansi
RUN composer install -q -n --no-dev
RUN composer install -q -n --no-scripts
RUN composer install -q -n --no-progress
RUN composer install -q -n --prefer-dist
RUN chmod -R 777 storage bootstrap/cache
RUN php artisan optimize:clear
RUN php artisan optimize
