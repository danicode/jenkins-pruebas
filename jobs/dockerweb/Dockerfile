FROM php:8.0-fpm-alpine
LABEL maintainer="danicode"

RUN apk add --no-cache \
    nginx \
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

# Configurar Nginx
RUN mkdir /run/nginx && \
    echo "server { \
        listen 80; \
        server_name localhost; \
        root /var/www/html; \
        index index.php index.html index.htm; \
        location / { \
            try_files \$uri \$uri/ /index.php?\$query_string; \
        } \
        location ~ \.php$ { \
            include fastcgi_params; \
            fastcgi_pass 127.0.0.1:9000; \
            fastcgi_index index.php; \
            fastcgi_param SCRIPT_FILENAME \$document_root\$fastcgi_script_name; \
        } \
    }" > /etc/nginx/conf.d/default.conf

CMD ["sh", "-c", "php-fpm & nginx -g 'daemon off;'"]
