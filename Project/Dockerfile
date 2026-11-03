FROM php:8.4-apache

RUN apt-get update && apt-get install -y \
    libzip-dev zip unzip \
    libpng-dev libjpeg-dev libfreetype6-dev \
    libonig-dev libxml2-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install pdo pdo_mysql mysqli mbstring zip gd fileinfo bcmath \
    && a2enmod rewrite headers \
    && rm -rf /var/lib/apt/lists/*

RUN echo "memory_limit = 256M" > /usr/local/etc/php/conf.d/hamarecrm.ini \
 && echo "upload_max_filesize = 100M" >> /usr/local/etc/php/conf.d/hamarecrm.ini \
 && echo "post_max_size = 100M" >> /usr/local/etc/php/conf.d/hamarecrm.ini \
 && echo "max_execution_time = 60" >> /usr/local/etc/php/conf.d/hamarecrm.ini \
 && echo "max_input_vars = 5000" >> /usr/local/etc/php/conf.d/hamarecrm.ini \
 && echo "date.timezone = Asia/Tehran" >> /usr/local/etc/php/conf.d/hamarecrm.ini

ENV APACHE_DOCUMENT_ROOT=/var/www/html/public
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf \
 && sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf \
 && sed -i '/<Directory \/var\/www\/>/,/<\/Directory>/ s/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf

WORKDIR /var/www/html
