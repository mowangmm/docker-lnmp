FROM php:7-fpm
RUN set -xe \
# "构建依赖"
    && buildDeps=" \
        build-essential \
        php5-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    " \
# "安装 php 以及编译构建组件所需包"
    && apt-get update \
    && apt-get install -y ${buildDeps} --no-install-recommends \
# "编译安装 php 组件"
    && docker-php-ext-install iconv mcrypt mysqli pdo pdo_mysql zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
# "清理"
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false -o APT::AutoRemove::SuggestsImportant=false $buildDeps \
    && rm -rf /var/cache/apt/* \
    && rm -rf /var/lib/apt/lists/*
