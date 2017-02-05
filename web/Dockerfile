FROM php:7-apache

# phpの設定ファイルを配置
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

# phpの拡張モジュール
RUN docker-php-ext-install iconv mbstring mcrypt mysqli pdo_mysql

# composerのインストール
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN a2enmod ssl rewrite
EXPOSE 443

# apacheの設定ファイルを配置
COPY apache/ /etc/apache2/sites-available/

# Apacheの設定を反映
RUN a2ensite ssl-default && a2ensite default

