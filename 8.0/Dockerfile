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
    && apt-get install -y php8.0-cli php8.0-dev \
    php8.0-pgsql php8.0-sqlite3 php8.0-gd \
    php8.0-curl \
    php8.0-imap php8.0-mysql php8.0-mbstring \
    php8.0-xml php8.0-zip php8.0-bcmath php8.0-soap \
    php8.0-intl php8.0-readline \
    php8.0-ldap \
    php8.0-msgpack php8.0-igbinary php8.0-redis php8.0-swoole \
    php8.0-memcached php8.0-pcov php8.0-xdebug \
    php8.0-imagick \
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

RUN update-alternatives --set php /usr/bin/php8.0

RUN setcap "cap_net_bind_service=+ep" /usr/bin/php8.0