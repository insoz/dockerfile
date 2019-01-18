FROM php:7.2.1-fpm-stretch

LABEL maintainer="Leon <nian0408@foxmail.com>"

COPY ./sources.list /etc/apt/sources.list

RUN apt-get update && apt-get install -y gnupg apt-transport-https procps net-tools lsof; \
    curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -; \
    curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list; \
    apt-get update; \
    apt-get install -y --no-install-recommends libfreetype6-dev libjpeg62-turbo-dev zlib1g-dev libpng-dev; \
    ACCEPT_EULA=Y apt-get install -y --no-install-recommends msodbcsql17; \
    ACCEPT_EULA=Y apt-get install -y --no-install-r\ecommends mssql-tools; \
    ACCEPT_EULA=Y apt-get install -y --no-install-recommends unixodbc-dev; \
    \
    docker-php-ext-install pdo gd pdo_mysql zip; \
    pecl channel-update pecl.php.net; \
    pecl install redis pdo_sqlsrv sqlsrv; \
    \
    docker-php-ext-enable redis gd pdo_mysql pdo_sqlsrv sqlsrv; \
    \
    rm -rf /var/lib/apt/lists/*; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false; \
    sed -i 's/clear_env = no/clear_env = yes/g' /usr/local/etc/php-fpm.d/docker.conf
