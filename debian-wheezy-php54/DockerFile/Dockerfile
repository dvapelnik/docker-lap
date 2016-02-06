# VERSION                   0.0.1

FROM eboraas/apache:wheezy

MAINTAINER Dmitry Vapelnik <dvapelnik@gmail.com>

RUN groupadd -g 1000 donkey && \
    useradd -u 1000 -g 1000 -G sudo donkey && \
    apt-get update && \
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
        php5-memcache \
        php5-memcached \
        php5-mysql \
        php5-pgsql \
        php5-sqlite \
        php5-xdebug \
        php5-xmlrpc \
        sudo \
    && \
    apt-get install -y php5-dev build-essential && \
    pecl install xdebug && \
    rm -f /etc/php5/cli/conf.d/*-xdebug.ini && \
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
    ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/ && \
    cat /etc/php5/mods-available/xdebug.ini >> /etc/php5/apache2/php.ini && \
    sed -i 's/export APACHE_RUN_USER=www-data/export APACHE_RUN_USER=donkey/' /etc/apache2/envvars && \
    sed -i 's/export APACHE_RUN_GROUP=www-data/export APACHE_RUN_GROUP=donkey/' /etc/apache2/envvars && \
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
    rm -rf /var/lib/apt/lists/*

COPY 30-xdebug.addition.ini /etc/php5/apache2/conf.d/30-xdebug.addition.ini
COPY start /start

USER donkey

WORKDIR /var/www

EXPOSE 80

CMD ["/usr/local/bin/gosu", "root", "/bin/bash", "/start"]
