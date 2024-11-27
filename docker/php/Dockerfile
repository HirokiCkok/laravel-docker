FROM php:8.2-fpm

# php.ini のコピー
COPY php.ini /usr/local/etc/php/

# 必要なパッケージのインストール
RUN apt-get update \
  && apt-get install -y zlib1g-dev mariadb-client vim libzip-dev \
  && docker-php-ext-install zip pdo_mysql

# Composer のインストール
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

# Composer の環境変数設定
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

# 作業ディレクトリ設定
WORKDIR /var/www

# Laravel インストーラーのインストール
RUN composer global require "laravel/installer"
