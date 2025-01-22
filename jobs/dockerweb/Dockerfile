# Utilizamos una imagen base de PHP 8 con Apache
FROM php:8.2-apache

# Establecemos el directorio de trabajo dentro del contenedor
WORKDIR /var/www/html

# Copiamos el código de la aplicación
COPY . .

# Instalamos extensiones PHP necesarias (ajusta según tus necesidades)
RUN docker-php-ext-install pdo_mysql mysqli

# Configuramos la zona horaria (opcional)
ENV TZ=America/Mexico
RUN ln -sf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Exponemos el puerto 80 para el acceso web
EXPOSE 80

# Iniciamos Apache en primer plano
CMD ["apache2-ctl", "-D", "FOREGROUND"]
