# VERSION                   0.0.1

FROM eboraas/apache:jessie

MAINTAINER Dmitry Vapelnik <dvapelnik@gmail.com>

RUN groupadd -g 1000 donkey \
    && \
    useradd -u 1000 -g 1000 -M donkey \
    && \
    apt-get update \
    && \
    apt-get install -y \
        sudo \
        git \
        php5 \
        php-apc \
        php5-memcache \
        php5-memcached \
        php-date \
        php-db \
        php-gettext \
        php5-imagick \
        php-services-json \
        php-soap \
        php-xajax \
        php5-cli \
        php5-common \
        php5-curl \
        php5-gd \
        php5-intl \
        php5-ldap \
        php5-mysql \
        php5-pgsql \
        php5-sqlite \
        php5-mcrypt \
        php5-xmlrpc \
        php5-xdebug \
    && \
    rm -f /etc/php5/cli/conf.d/*-xdebug.ini \
    && \
    apt-get autoremove -y && apt-get clean \
    && \
    ln -s ../mods-available/rewrite.load /etc/apache2/mods-enabled/ && \
    ln -s ../mods-available/socache_shmcb.load /etc/apache2/mods-enabled/ && \
    ln -s ../sites-available/000-default.conf /etc/apache2/sites-enabled/000-default && \
    rm -f /etc/apache2/sites-enabled/000-default.conf \
    && \
    rm -rf /var/www/html && \
    rm -f /etc/apache2/sites-enabled/001-default-ssl && \
    sed -i 's/export APACHE_RUN_USER=www-data/export APACHE_RUN_USER=donkey/' /etc/apache2/envvars && \
    sed -i 's/export APACHE_RUN_GROUP=www-data/export APACHE_RUN_GROUP=donkey/' /etc/apache2/envvars && \
    sed -i 's/\/var\/www\/html/\/var\/www/' /etc/apache2/sites-available/000-default.conf && \
    sed -i 's/IncludeOptional conf\-enabled\/\*\.conf/IncludeOptional conf\-enabled\/\*/' /etc/apache2/apache2.conf && \
    sed -i 's/IncludeOptional sites\-enabled\/\*\.conf/IncludeOptional sites\-enabled\/\*/' /etc/apache2/apache2.conf && \
    sed -i 's/html_errors = Off/html_errors = On/' /etc/php5/apache2/php.ini && \
    sed -i 's/implicit_flush = Off/implicit_flush = On/' /etc/php5/apache2/php.ini

ADD xdebug.addition.ini /etc/php5/apache2/conf.d/xdebug.addition.ini
ADD start /start

USER donkey

WORKDIR /var/www

CMD ["/bin/bash", "/start"]
