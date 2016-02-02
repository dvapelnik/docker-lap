# VERSION                   0.2.0

FROM ubuntu-debootstrap:trusty

MAINTAINER Dmitry Vapelnik <dvapelnik@gmail.com>

ADD sources.list /etc/apt/sources.list

RUN groupadd -g 1000 donkey && \
    useradd -u 1000 -g 1000 -M donkey && \
    apt-get update && \
    apt-get install -y python-software-properties software-properties-common && \
    locale-gen en_US.UTF-8 && export LANG=en_US.UTF-8 && \
    add-apt-repository -y ppa:ondrej/php-7.0 && \
    apt-get update && \
    apt-get install -y \
        apache2 \
        sudo \
        git \
        wget \
        build-essential \
        php7.0-common \
        libapache2-mod-php7.0 \
        php7.0-cli \
        libphp7.0-embed \
        php7.0-dev \
        php7.0-curl \
        php7.0-enchant \
        php7.0-gd \
        php7.0-intl \
        php7.0-mcrypt \
        php7.0-readline \
        php7.0-odbc \
        php7.0-pgsql \
        php7.0-recode \
        php7.0-tidy \
        php7.0-xmlrpc \
        php7.0-xsl \
        php7.0 \
        php7.0-json \
        php7.0-sqlite3 \
        php7.0-mysql \
        php7.0-bz2 \
    && \
    apt-get autoremove -y && apt-get clean && \
    cd /tmp && \
    wget http://xdebug.org/files/xdebug-2.4.0rc2.tgz && \
    tar -xzf xdebug-2.4.0rc2.tgz && \
    cd xdebug-2.4.0RC2 && \
    phpize && ./configure --enable-xdebug && make && make install && \
    printf "[xdebug]\nzend_extension=xdebug.so\n" > /etc/php/mods-available/xdebug.ini && \
    ln -s /etc/php/mods-available/xdebug.ini /etc/php/7.0/apache2/conf.d/20-xdebug.ini && \
    cd / && \
    rm -rf xdebug-2.4.0rc2.tgz tar xdebug-2.4.0rc2.tgz && \
    ln -sf ../mods-available/rewrite.load /etc/apache2/mods-enabled/ && \
    ln -sf ../sites-available/000-default.conf /etc/apache2/sites-enabled/000-default && \
    rm -f /etc/apache2/sites-enabled/000-default.conf && \
    rm -rf /var/www/html && \
    sed -i 's/export APACHE_RUN_USER=www-data/export APACHE_RUN_USER=donkey/' /etc/apache2/envvars && \
    sed -i 's/export APACHE_RUN_GROUP=www-data/export APACHE_RUN_GROUP=donkey/' /etc/apache2/envvars && \
    sed -i 's/\/var\/www\/html/\/var\/www/' /etc/apache2/sites-available/000-default.conf && \
    sed -i 's/IncludeOptional conf\-enabled\/\*\.conf/IncludeOptional conf\-enabled\/\*/' /etc/apache2/apache2.conf && \
    sed -i 's/IncludeOptional sites\-enabled\/\*\.conf/IncludeOptional sites\-enabled\/\*/' /etc/apache2/apache2.conf && \
    sed -i 's/implicit_flush = Off/implicit_flush = On/' /etc/php/7.0/apache2/php.ini && \
    sed -i 's/expose_php = On/expose_php = Off/' /etc/php/7.0/apache2/php.ini && \
    sed -i 's/;date.timezone\s=/date.timezone = Europe\/Kiev/' /etc/php/7.0/apache2/php.ini && \
    phpenmod mcrypt

EXPOSE 80

ADD 30-xdebug.addition.ini /etc/php/7.0/apache2/conf.d/30-xdebug.addition.ini

USER donkey

WORKDIR /var/www

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
