FROM php:7.2.1-fpm-stretch

LABEL maintainer="Leon <nian0408@foxmail.com>"

ENV REDIS-VERSION="4.2.0"

RUN apt-get update && apt-get install -y gnupg apt-transport-https; \
    curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -; \
	curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list; \
	apt-get update; \
	apt-get install -y --no-install-recommends libargon2-dev msodbcsql17; \
    ACCEPT_EULA=Y apt-get install -y --no-install-recommends mssql-tools; \
	ACCEPT_EULA=Y apt-get install -y --no-install-recommends unixodbc-dev; \
    \
    curl -fsSL https://github.com/phpredis/phpredis/archive/$REDIS-VERSION.tar.gz -o redis.tar.gz; \
    mkdir -p /tmp/redis; \
    tar -xf redis.tar.gz -C /tmp/redis --strip-components=1; \
    rm redis.tar.gz; \
    docker-php-ext-configure /tmp/redis --enable-redis; \
    docker-php-ext-install /tmp/redis; \
    rm -r /tmp/redis; \
    \
    pecl install pdo_mysql; \
    pecl install sqlsrv; \
    pecl install pdo_sqlsrv; \
    docker-php-ext-enable pdo_sqlsrv sqlsrv; \
    rm -rf /var/lib/apt/lists/*; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false
