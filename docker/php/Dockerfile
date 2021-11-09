FROM php:7.2-fpm

#Set timezone Asia/Ho_Chi_Minh
ENV TZ='Asia/Ho_Chi_Minh'
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install package
RUN apt-get update
RUN apt-get install vim git zip unzip libpng-dev libzip-dev librabbitmq-dev libicu-dev cron -y

# Database
RUN pecl install mongodb \
	&& docker-php-ext-enable mongodb
RUN docker-php-ext-install pdo_mysql zip bcmath gd opcache
RUN pecl install amqp \
    && docker-php-ext-enable amqp

# Imap
RUN apt-get install libkrb5-dev libc-client-dev -y
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl
RUN docker-php-ext-install imap

# Intl
RUN apt-get install zlib1g-dev libicu-dev -y
RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl

# Timezone
RUN echo "date.timezone = Asia/Ho_Chi_Minh" >> /usr/local/etc/php/php.ini
RUN echo "memory_limit = 1024M" >> /usr/local/etc/php/php.ini
RUN sed -i 's/pm.max_children = 5/pm.max_children = 30/g' /usr/local/etc/php-fpm.d/www.conf

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www

RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

CMD ["php-fpm"]

EXPOSE "9000"
