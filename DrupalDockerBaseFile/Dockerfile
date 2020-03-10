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

# Docker Compose with glibc bypass.
RUN curl -Lo glibc.apk https://github.com/WSauvan/DrupalDockerFile/raw/master/glibc-2.23-r3.apk && \
    curl -Lo glibc-bin.apk https://github.com/WSauvan/DrupalDockerFile/raw/master/glibc-bin-2.23-r3.apk && \
    apk add --allow-untrusted glibc.apk glibc-bin.apk

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
RUN ln -s /etc/php7 /etc/php && \
    mv /usr/bin/php /usr/bin/php5 && \
    ln -s /usr/bin/php7 /usr/bin/php && \
    ln -s /usr/sbin/php-fpm7 /usr/bin/php-fpm && \
    ln -s /usr/lib/php7 /usr/lib/php

# Install Composer.
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Install Docker Compose.
RUN curl -Lo docker-compose https://github.com/docker/compose/releases/download/1.8.1/docker-compose-Linux-x86_64 && \
    chmod +x docker-compose && \
    mv docker-compose /usr/local/bin

# Security fix for CVE-2016-0777 and CVE-2016-0778
RUN echo -e 'Host *\nUseRoaming no' >> /etc/ssh/ssh_config

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["sh"]
