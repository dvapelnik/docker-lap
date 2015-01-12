# VERSION                   0.1.0

FROM ubuntu-debootstrap:trusty

MAINTAINER Dmitry Vapelnik <dvapelnik@gmail.com>

ADD sources.list /etc/apt/sources.list

RUN groupadd -g 1000 donkey \
    && \
    useradd -u 1000 -g 1000 -M donkey \
    && \
    apt-get update \
    && \
    apt-get install -y memcached \
    && \
    apt-get install -y apache2 \
    && \
    apt-get install -y \
        php5 \
        php-apc \
        php5-memcache \
        php5-memcached \
        php5-mcrypt \
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
    apt-get autoremove -y && apt-get clean \
    && \
    ln -sf ../mods-available/rewrite.load /etc/apache2/mods-enabled/ && \
    ln -sf ../sites-available/000-default.conf /etc/apache2/sites-enabled/000-default && \
    rm -f /etc/apache2/sites-enabled/000-default.conf \
    && \
    rm -rf /var/www/html && \
    sed -i 's/export APACHE_RUN_USER=www-data/export APACHE_RUN_USER=donkey/' /etc/apache2/envvars && \
    sed -i 's/export APACHE_RUN_GROUP=www-data/export APACHE_RUN_GROUP=donkey/' /etc/apache2/envvars && \
    sed -i 's/\/var\/www\/html/\/var\/www/' /etc/apache2/sites-available/000-default.conf && \
    sed -i 's/IncludeOptional conf\-enabled\/\*\.conf/IncludeOptional conf\-enabled\/\*/' /etc/apache2/apache2.conf && \
    sed -i 's/IncludeOptional sites\-enabled\/\*\.conf/IncludeOptional sites\-enabled\/\*/' /etc/apache2/apache2.conf && \
    sed -i 's/implicit_flush = Off/implicit_flush = On/' /etc/php5/apache2/php.ini && \
    sed -i 's/expose_php = On/expose_php = Off/' /etc/php5/apache2/php.ini && \
    php5enmod mcrypt

EXPOSE 80

ADD 30-xdebug.addition.ini /etc/php5/apache2/conf.d/30-xdebug.addition.ini
ADD start /start

CMD ["/bin/bash", "/start"]
