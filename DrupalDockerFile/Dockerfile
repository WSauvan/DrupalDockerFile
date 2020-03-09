FROM composer:latest

# Install php-gd
RUN apk add --repository http://dl-cdn.alpinelinux.org/alpine/edge/main libpng-dev && docker-php-ext-install gd && rm -rf /var/cache/apk/*

# Make Composer install times bearable
RUN composer global require "squizlabs/php_codesniffer=*"
RUN composer global require drupal/coder
RUN composer global require dealerdirect/phpcodesniffer-composer-installer
RUN ln -s ~/.composer/vendor/bin/phpcs /usr/local/bin
RUN phpcs --config-set installed_paths ~/.composer/vendor/drupal/coder/coder_sniffer

# Make Composer install times bearable
RUN composer global require hirak/prestissimo

# Download and install Drush launcher
RUN php -r "copy('https://github.com/drush-ops/drush-launcher/releases/download/0.4.2/drush.phar', 'drush.phar');" && chmod +x drush.phar && mv drush.phar /usr/bin/drush
