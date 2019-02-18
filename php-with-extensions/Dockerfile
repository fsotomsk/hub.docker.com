FROM php:7.3-cli-stretch

RUN mkdir /app && \
    buildDeps="libpq-dev libzip-dev libicu-dev libpng-dev libjpeg62-turbo-dev libfreetype6-dev libmagickwand-6.q16-dev git-core ssh zlib1g-dev" && \
    apt-get update && \
    apt-get install -y $buildDeps --no-install-recommends && \
    ln -s /usr/lib/x86_64-linux-gnu/ImageMagick-6.8.9/bin-Q16/MagickWand-config /usr/bin && \
    pecl install imagick && \
    echo "extension=imagick.so" > /usr/local/etc/php/conf.d/ext-imagick.ini && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    docker-php-ext-install \
        pdo \
        pdo_pgsql \
        pgsql \
        sockets \
        zip \
        bcmath \
        opcache \
        intl && \
    git clone -b master https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis && \
    docker-php-ext-install \
        redis && \
    pecl install inotify && \
    echo "extension=inotify.so" > /usr/local/etc/php/conf.d/ext-inotify.ini && \
    pecl install swoole && \
    echo "extension=swoole.so" > /usr/local/etc/php/conf.d/ext-swoole.ini && \
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/local/sbin --filename=composer && \
    php -r "unlink('composer-setup.php');"

CMD ["php"]
