FROM php:7.4-fpm

RUN apt-get update && apt-get install -y git curl zip unzip libxml2-dev
RUN apt-get install -y xvfb
RUN apt-get install -y libxslt-dev

RUN apt-get install -y libreoffice \
                       libreoffice-writer \
                       libreoffice-java-common \
                       libreoffice-core \
                       libreoffice-common \
                       default-jre

RUN apt-get install -y libicu-dev

# Install zip
RUN apt-get install -y \
        libzip-dev \
        && docker-php-ext-install zip

RUN docker-php-ext-install pdo pdo_mysql
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ENV COMPOSER_CACHE_DIR=/.cache/composer

RUN apt-get install -y default-mysql-client --fix-missing
RUN apt-get install -y poppler-utils

RUN curl -sL https://deb.nodesource.com/setup_lts.x | bash -
RUN apt-get install -y nodejs

RUN apt-get install -y libtidy-dev

# Install Redis
RUN apt-get install -y redis-server

RUN apt-get -y --no-install-recommends install php7.4-mysql php-ssh2 build-essential zlib1g-dev g++ rsync openssl ssh

# Install PHP extensions
RUN docker-php-ext-configure tidy
RUN docker-php-ext-install tidy
RUN docker-php-ext-install pdo pdo_mysql
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl
RUN docker-php-ext-configure bcmath --enable-bcmath
RUN docker-php-ext-install bcmath
RUN docker-php-ext-configure soap --enable-soap
RUN docker-php-ext-install soap
RUN docker-php-ext-configure sysvsem --enable-sysvsem
RUN docker-php-ext-install sysvsem
RUN docker-php-ext-configure pcntl --enable-pcntl \
&& docker-php-ext-install pcntl
RUN docker-php-ext-install xsl
RUN pecl install -o -f redis \
&&  rm -rf /tmp/pear \
&&  docker-php-ext-enable redis

# Install imagick
RUN apt-get update && apt-get install -y \
    libmagickwand-dev --no-install-recommends
RUN pecl install imagick && docker-php-ext-enable imagick

# Install GD
RUN apt-get update \
&& apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
&& docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
&& docker-php-ext-install gd

# Config
RUN mkdir -p /.cache/dconf \
&& chmod -R 777 /.cache/ \
&& chmod -R 777 /usr/bin/loffice

WORKDIR "/application"