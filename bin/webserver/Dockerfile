FROM php:7.1-apache

RUN apt-get clean && apt-get -y update --fix-missing && apt-get upgrade -y

# Install important libraries
RUN apt-get -y install --fix-missing apt-utils  \
                      build-essential  \
                      git  \
                      curl  \
                      libcurl3  \
                      libcurl3-dev  \
                      zip  \
                      vim  \
                      sudo \
                      wget


# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install xdebug
RUN pecl install xdebug-2.5.0 && docker-php-ext-enable xdebug

# Other PHP7 Extensions

RUN apt-get -y install libmcrypt-dev  \
                      libsqlite3-dev  \
                      libsqlite3-0  \
                      mysql-client  \
                      zlib1g-dev  \
                      libicu-dev  \
                      libfreetype6-dev  \
                      libjpeg62-turbo-dev  \
                      libpng12-dev
RUN docker-php-ext-install mcrypt  \
                      pdo  \
                      pdo_mysql  \
                      mysqli  \
                      pdo_sqlite  \
                      curl  \
                      tokenizer  \
                      json  \
                      zip  \
                      -j$(nproc) intl  \
                      mbstring  \
                      bcmath

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd

# Enable apache modules
RUN a2enmod rewrite headers
