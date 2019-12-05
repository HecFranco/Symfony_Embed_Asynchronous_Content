FROM php:7.3.12-fpm

MAINTAINER Héctor Franco Aceituno <hector.franco.aceituno@mail.com>

ARG timezone

RUN apt-get update && apt-get install --no-install-recommends --no-install-suggests -y \
  git \
  unzip \
  libicu-dev \
  zlib1g-dev \
  libssl-dev \
  pkg-config \
  libpq-dev \
  && rm -rf /var/lib/apt/lists/*

RUN set -xe \
  && docker-php-ext-configure \
  intl \
  && docker-php-ext-install \
  intl \
  opcache \
  # zip \
  pdo \
  pdo_mysql \
  pdo_pgsql \
  && pecl install \
  apcu \
  xdebug \
  mongodb \
  redis \
  && docker-php-ext-enable \
  apcu \
  xdebug \
  mongodb \
  redis

COPY php.ini /usr/local/etc/php/php.ini
RUN sed -i -e "s#TIMEZONE#$timezone#g" /usr/local/etc/php/php.ini

#################################################################
# INSTALL XDEBUG
COPY xdebug.ini /tmp/xdebug.ini
RUN cat /tmp/xdebug.ini >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN rm /tmp/xdebug.ini
#################################################################

#################################################################
# INSTALL COMPOSER
COPY --from=composer:1.6 /usr/bin/composer /usr/bin/composer
# https://getcomposer.org/doc/03-cli.md#composer-allow-superuser
ENV COMPOSER_ALLOW_SUPERUSER 1
# create composer cache directory
# RUN mkdir -p /var/www/.composer && chown -R www-data /var/www/.composer
# add this command line to change the write permissions to the cache folder
RUN mkdir -p /var/cache && chown -R www-data /var/cache
#################################################################

#################################################################
# INSTALL NODEJS AND NPM
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash \
      && apt-get install -y nodejs npm
#################################################################

# RUN usermod -u 1000 www-data

# Change www-data user to match the host system UID and GID and chown www directory
RUN usermod --non-unique --uid 1000 www-data \
  && groupmod --non-unique --gid 1000 www-data \
  && chown -R www-data:www-data /var/cache

WORKDIR /srv
