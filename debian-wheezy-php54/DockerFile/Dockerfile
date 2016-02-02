# VERSION                   0.0.1

FROM eboraas/apache:wheezy

MAINTAINER Dmitry Vapelnik <dvapelnik@gmail.com>

RUN groupadd -g 1000 donkey \
    && \
    useradd -u 1000 -g 1000 -M donkey \
    && \
    apt-get update \
    && \
    apt-get install -y \
        git \
        sudo \
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
    apt-get install -y php5-dev build-essential \
    && \
    pecl install xdebug \
    && \
    rm -f /etc/php5/cli/conf.d/*-xdebug.ini \
    && \
    apt-get autoremove -y \
        autoconf \
        automake \
        autotools-dev \
        binutils \
        build-essential \
        bzip2 \
        cpp \
        cpp-4.7 \
        dpkg-dev \
        fakeroot \
        g++ \
        g++-4.7 \
        gcc \
        gcc-4.7 \
        libalgorithm-diff-perl \
        libalgorithm-diff-xs-perl \
        libalgorithm-merge-perl \
        libc-dev-bin \
        libc6-dev \
        libdpkg-perl \
        libfile-fcntllock-perl \
        libgmp10 \
        libitm1 \
        libltdl-dev \
        libmpc2 \
        libmpfr4 \
        libquadmath0 \
        libssl-dev \
        libssl-doc \
        libstdc++6-4.7-dev \
        libtimedate-perl \
        libtool \
        linux-libc-dev \
        m4 \
        make \
        manpages \
        manpages-dev \
        patch \
        php5-dev \
        shtool \
        zlib1g-dev \
    && \
    apt-get autoremove -y && apt-get clean \
    && \
    ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/ \
    && \
    cat /etc/php5/mods-available/xdebug.ini >> /etc/php5/apache2/php.ini \
    && \
    sed -i 's/export APACHE_RUN_USER=www-data/export APACHE_RUN_USER=donkey/' /etc/apache2/envvars && \
    sed -i 's/export APACHE_RUN_GROUP=www-data/export APACHE_RUN_GROUP=donkey/' /etc/apache2/envvars && \
    sed -i 's/implicit_flush = Off/implicit_flush = On/' /etc/php5/apache2/php.ini && \
    sed -i 's/expose_php = On/expose_php = Off/' /etc/php5/apache2/php.ini

ADD 30-xdebug.addition.ini /etc/php5/apache2/conf.d/30-xdebug.addition.ini
ADD start /start

USER donkey

WORKDIR /var/www

CMD ["/bin/bash", "/start"]
