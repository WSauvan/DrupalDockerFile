FROM docker

# Custom additions for test runner.
RUN apk --update add \
    bash \
    ca-certificates \
    curl \
    git \
    make \
    openssh-client \
    patch \
    tar

# Install PHP.
RUN apk --no-cache --update --repository=http://dl-cdn.alpinelinux.org/alpine/edge/main add \
    libressl && \
    apk --no-cache --update --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community add \
    php7 \
    php7-xml \
    php7-xsl \
    php7-pdo_mysql \
    php7-mcrypt \
    php7-curl \
    php7-json \
    php7-fpm \
    php7-phar \
    php7-openssl \
    php7-mysqli \
    php7-ctype \
    php7-opcache \
    php7-mbstring \
    php7-zip \
    php7-zlib

# Correct paths.
RUN mv /etc/php /etc/php5
RUN ln -s /etc/php7 /etc/php
RUN ln -s /usr/bin/php7 /usr/bin/php
RUN ln -s /usr/sbin/php-fpm7 /usr/bin/php-fpm
RUN ln -s /usr/lib/php7 /usr/lib/php

# Install Composer.
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

COPY docker-entrypoint.sh /usr/local/bin/

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["sh"]
