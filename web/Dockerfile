FROM php:7-apache

# php$B$N@_Dj%U%!%$%k$rG[CV(B
COPY php/php.ini-development $PHP_INI_DIR/php.ini
COPY php/conf.d/ $PHP_INI_DIR/conf.d/

RUN \
  apt-get update && apt-get install -y \
    curl \
    git \
    libmcrypt-dev \
    libxml2-dev \
    man \
    ssl-cert \
    vim \
  --no-install-recommends && rm -r /var/lib/apt/lists/*

# php$B$N3HD%%b%8%e!<%k(B
RUN docker-php-ext-install iconv mbstring mcrypt mysqli pdo_mysql

# composer$B$N%$%s%9%H!<%k(B
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN a2enmod ssl rewrite
EXPOSE 443

# apache$B$N@_Dj%U%!%$%k$rG[CV(B
COPY apache/ /etc/apache2/sites-available/

# Apache$B$N@_Dj$rH?1G(B
RUN a2ensite ssl-default && a2ensite default

