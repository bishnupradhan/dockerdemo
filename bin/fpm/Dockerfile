FROM php:7.1-fpm

RUN apt-get clean && apt-get -y update --fix-missing && apt-get upgrade -y

RUN apt-get -y install git \
    g++ libcurl4-gnutls-dev libicu-dev libmcrypt-dev libpq-dev libxml2-dev unzip zlib1g-dev \
    && git clone -b 3.0.0 https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis \ 
    && docker-php-ext-install pdo redis xml mcrypt



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

RUN apt-get autoremove && apt-get autoclean \
      && rm -rf /var/lib/apt/lists/*