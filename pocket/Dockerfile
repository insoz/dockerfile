FROM php:7.2.1-fpm-stretch

LABEL maintainer="Leon <nian0408@foxmail.com>"

# COPY ./sources.list /etc/apt/sources.list
COPY ./php.ini /usr/local/etc/php/conf.d/php.ini

RUN apt-get update && apt-get install -y procps net-tools lsof vim; \
    apt-get install -y --no-install-recommends libfreetype6-dev libjpeg62-turbo-dev zlib1g-dev libpng-dev; \
    curl -sSL https://github.com/alexeyrybak/blitz/archive/0.10.4-PHP7.tar.gz -o blitz.tar.gz; \
    mkdir -p /tmp/blitz; \
    tar -xf blitz.tar.gz -C /tmp/blitz --strip-components=1; \
    rm blitz.tar.gz; \
    docker-php-ext-configure /tmp/blitz; \
    docker-php-ext-install /tmp/blitz; \
    rm -r /tmp/blitz; \
    docker-php-ext-install pdo gd pdo_mysql zip mysqli; \
    pecl channel-update pecl.php.net; \
    pecl install redis igbinary yaf; \
    \
    docker-php-ext-enable redis gd pdo_mysql igbinary yaf mysqli; \
    \
    rm -rf /var/lib/apt/lists/*; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false; \
    sed -i "s/clear_env = no/clear_env = yes/g" /usr/local/etc/php-fpm.d/docker.conf; \
    echo "php_flag[display_errors] = on" >> /usr/local/etc/php-fpm.d/www.conf; \
    echo "php_admin_value[memory_limit] = 128M" >> /usr/local/etc/php-fpm.d/www.conf; \
    echo "php_admin_flag[log_errors] = on" >> /usr/local/etc/php-fpm.d/www.conf;