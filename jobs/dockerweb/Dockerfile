FROM php:8.0-apache
LABEL maintainer="danicode"

RUN apk add --no-cache \
    zlib-dev \
    icu-dev \
    libxml2-dev \
    postgresql-dev \
    vim && \
    docker-php-ext-configure pgsql --with-pgsql=/usr/local/pgsql && \
    docker-php-ext-install pdo pdo_mysql pdo_pgsql zip intl xmlrpc soap opcache && \
    docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd

COPY . /var/www/html/
WORKDIR /var/www/html/
