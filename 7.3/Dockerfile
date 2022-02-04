FROM ubuntu:21.10

LABEL maintainer="John Michael Manlupig"

ARG WWWGROUP
ARG NODE_VERSION=16

ENV DEBIAN_FRONTEND noninteractive
ENV TZ=UTC

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update \
    && apt-get install -y nano gnupg gosu curl ca-certificates zip unzip git supervisor sqlite3 libcap2-bin libpng-dev python2 \
    && apt install -y software-properties-common \
    && add-apt-repository -y ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y php7.3-cli php7.3-dev \
    php7.3-pgsql php7.3-sqlite3 php7.3-gd \
    php7.3-curl \
    php7.3-imap php7.3-mysql php7.3-mbstring \
    php7.3-xml php7.3-zip php7.3-bcmath php7.3-soap \
    php7.3-intl php7.3-readline \
    php7.3-ldap \
    php7.3-msgpack php7.3-igbinary php7.3-redis php7.3-swoole \
    php7.3-memcached php7.3-pcov php7.3-xdebug \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && curl -sL https://deb.nodesource.com/setup_$NODE_VERSION.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g npm \
    && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" > /etc/apt/sources.list.d/yarn.list \
    && apt-get update \
    && apt-get install -y yarn \
    && apt-get install -y mysql-client \
    && apt-get install -y postgresql-client \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN setcap "cap_net_bind_service=+ep" /usr/bin/php7.3
