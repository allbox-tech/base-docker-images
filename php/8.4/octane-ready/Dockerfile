FROM php:8.4-alpine AS base

COPY --from=ghcr.io/mlocati/php-extension-installer:2.7 /usr/bin/install-php-extensions /usr/local/bin/

COPY --from=composer:2.8 /usr/bin/composer /usr/local/bin/composer

RUN install-php-extensions soap bcmath zip redis pcntl swoole pdo_mysql

RUN apk add --update nano curl



FROM base AS dev_base

ARG user
ARG uid

# Install nodejs and npm to use chokidar for octane watch
RUN apk add --update nodejs npm

# Use the same user as hosts user to prevent permission issues
RUN addgroup -g $uid $user \
  && adduser -u $uid -D -G $user -G www-data -G root $user \
  && mkdir -p /home/$user/.composer \
  && chown -R $user:$user /home/$user
