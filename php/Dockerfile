FROM php:5.5.36-fpm
RUN apt-get update
RUN apt-get install vim -y

# Install dependent for php extensions
RUN apt-get install -y \
    libpq-dev \
    libmemcached-dev \
    curl \
    libpng12-dev \
    libfreetype6-dev \
    --no-install-recommends \
    libmcrypt-dev \
    libxml2-dev \
    libbz2-dev \
    libldap2-dev \
    libldb-dev \
    && rm -r /var/lib/apt/lists/*

RUN docker-php-ext-configure gd \
    --enable-gd-native-ttf \
    --with-freetype-dir=/usr/include/freetype2

RUN ln -s /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/libldap.so \
		&& ln -s /usr/lib/x86_64-linux-gnu/liblber.so /usr/lib/liblber.so

# Install extensions using the helper script provided by the base image
RUN docker-php-ext-install \
    pdo_mysql \
    pdo_pgsql \
    gd \
    mcrypt \
    xml \
    bz2 \
    mysql \
    mysqli \
    soap \
    sockets \ 
    opcache \
    pgsql \
    pcntl \
    ldap \
    zip

# Install mcrypt
#RUN apt-get install php5-mcrypt -y

# Install memcached
RUN pecl install memcached -y && docker-php-ext-enable memcached 

# Install xdebug
RUN pecl install xdebug && docker-php-ext-enable xdebug

# Install mongodb driver
RUN pecl install mongo && docker-php-ext-enable mongo

# Install zookeeper ext
RUN apt-get install libzookeeper-mt-dev
RUN pecl install zookeeper channel://pecl.php.net/zookeeper-0.2.2 && docker-php-ext-enable zookeeper

# link nginx
RUN sed -i "164c listen = devPHP" /usr/local/etc/php-fpm.d/www.conf

RUN usermod -u 1000 www-data

# install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

#cp php.ini
RUN cp /usr/src/php/php.ini-development /usr/src/php/php.ini

EXPOSE 9000