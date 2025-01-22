FROM php:8.0-fpm-alpine
LABEL maintainer="danicode"

RUN apk add --no-cache \
    apache2 \
    apache2-proxy \
    apache2-ssl \
    apache2-http2 \
    apache2-utils \
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

# Configurar Apache
RUN echo "ServerName localhost" >> /etc/apache2/httpd.conf && \
    sed -i 's/\/var\/www\/localhost\/htdocs/\/var\/www\/html/g' /etc/apache2/httpd.conf && \
    sed -i 's/AllowOverride None/AllowOverride All/g' /etc/apache2/httpd.conf

CMD ["httpd", "-D", "FOREGROUND"]
