# VERSION                   0.2.0

FROM ubuntu-debootstrap:trusty

MAINTAINER Dmitry Vapelnik <dvapelnik@gmail.com>

ADD sources.list /etc/apt/sources.list

RUN groupadd -g 1000 donkey && \
    useradd -u 1000 -g 1000 -G sudo donkey && \
    apt-get update && \
    apt-get install -y apache2 && \
    apt-get install -y \
        curl \
        git \
        php-apc \
        php-date \
        php-db \
        php-gettext \
        php-services-json \
        php-soap \
        php-xajax \
        php5 \
        php5-cli \
        php5-common \
        php5-curl \
        php5-gd \
        php5-imagick \
        php5-intl \
        php5-ldap \
        php5-mcrypt \
        php5-mcrypt \
        php5-memcache \
        php5-memcached \
        php5-mysql \
        php5-pgsql \
        php5-sqlite \
        php5-xdebug \
        php5-xmlrpc \
        sudo \
    && \
    rm -f /etc/php5/cli/conf.d/*-xdebug.ini && \
    ln -sf ../mods-available/rewrite.load /etc/apache2/mods-enabled/ && \
    ln -sf ../sites-available/000-default.conf /etc/apache2/sites-enabled/000-default && \
    rm -f /etc/apache2/sites-enabled/000-default.conf && \
    rm -rf /var/www/html && \
    sed -i 's/export APACHE_RUN_USER=www-data/export APACHE_RUN_USER=donkey/' /etc/apache2/envvars && \
    sed -i 's/export APACHE_RUN_GROUP=www-data/export APACHE_RUN_GROUP=donkey/' /etc/apache2/envvars && \
    sed -i 's/\/var\/www\/html/\/var\/www/' /etc/apache2/sites-available/000-default.conf && \
    sed -i 's/IncludeOptional conf\-enabled\/\*\.conf/IncludeOptional conf\-enabled\/\*/' /etc/apache2/apache2.conf && \
    sed -i 's/IncludeOptional sites\-enabled\/\*\.conf/IncludeOptional sites\-enabled\/\*/' /etc/apache2/apache2.conf && \
    sed -i 's/implicit_flush = Off/implicit_flush = On/' /etc/php5/apache2/php.ini && \
    sed -i 's/expose_php = On/expose_php = Off/' /etc/php5/apache2/php.ini && \
    echo 'donkey ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers && \
    curl -o /usr/local/bin/gosu -sSL "https://github.com/tianon/gosu/releases/download/1.6/gosu-$(dpkg --print-architecture)" && \
    chown root:donkey /usr/local/bin/gosu && \
    chmod +x /usr/local/bin/gosu && \
    chmod +s /usr/local/bin/gosu && \
    apt-get purge curl -y && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    php5enmod mcrypt

EXPOSE 80

ADD 30-xdebug.addition.ini /etc/php5/apache2/conf.d/30-xdebug.addition.ini

USER donkey

WORKDIR /var/www

EXPOSE 80

CMD ["/usr/local/bin/gosu", "root", "/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
