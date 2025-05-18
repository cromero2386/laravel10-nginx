# Usa una imagen base de PHP 8.2-fpm-alpine
FROM php:8.2-fpm-alpine

# Copia configuración de PHP-FPM
ADD ./www.conf /usr/local/etc/php-fpm.d/www.conf

# Configura grupo y crea usuario
RUN addgroup -g 1001 laravel && adduser -G laravel -g laravel -u 1001 -s /bin/sh -D laravel


# Crea directorio del proyecto
RUN mkdir -p /var/www/html

# Cambia propietario del directorio del proyecto a laravel
RUN chown -R laravel:laravel /var/www/html

# Instala extensiones de PHP necesarias
RUN docker-php-ext-install pdo pdo_mysql

# Instala Composer globalmente
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Cambia al usuario laravel
USER laravel

# Directorio de trabajo
WORKDIR /var/www/html

