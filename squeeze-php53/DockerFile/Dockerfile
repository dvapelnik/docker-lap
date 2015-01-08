# VERSION                   0.0.1

FROM eboraas/apache:squeeze

MAINTAINER Dmitry Vapelnik <dvapelnik@gmail.com>

RUN groupadd -g 1000 donkey \
    && \
    useradd -u 1000 -g 1000 -M donkey \
    && \
    apt-get update \
    && \
    apt-get install -y memcached \
    && \
    apt-get install -y \
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
    apt-get remove -y \
        build-essential \
        bzip2 \
        dpkg-dev \
        fakeroot \
        g++ \
        g++-4.4 \
        libalgorithm-diff-perl \
        libalgorithm-diff-xs-perl \
        libalgorithm-merge-perl \
        libdpkg-perl \
        libstdc++6-4.4-dev \
        libtimedate-perl \
        make \
        patch \
        autoconf \
        automake \
        autotools-dev \
        binutils \
        cpp \
        cpp-4.4 \
        gcc \
        gcc-4.4 \
        libc-dev-bin \
        libc6-dev \
        libgmp3c2 \
        libltdl-dev \
        libmpfr4 \
        libssl-dev \
        libtool \
        linux-libc-dev \
        m4 \
        manpages \
        manpages-dev \
        php5-dev \
        shtool \
        zlib1g-dev\
    && \
    apt-get autoremove -y && apt-get clean \
    && \
    ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/ \
    && \
    sed -i 's/export APACHE_RUN_USER=www-data/export APACHE_RUN_USER=donkey/' /etc/apache2/envvars && \
    sed -i 's/export APACHE_RUN_GROUP=www-data/export APACHE_RUN_GROUP=donkey/' /etc/apache2/envvars && \
    sed -i 's/html_errors = Off/html_errors = On/' /etc/php5/apache2/php.ini && \
    sed -i 's/implicit_flush = Off/implicit_flush = On/' /etc/php5/apache2/php.ini

ADD xdebug.addition.ini /etc/php5/apache2/conf.d/xdebug.addition.ini
ADD start /start

CMD ["/bin/bash", "/start"]