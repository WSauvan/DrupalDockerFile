FROM drupalwxt/gitlab-ci

# Make Composer install times bearable
RUN composer global require "squizlabs/php_codesniffer=*"
RUN composer global require drupal/coder
RUN composer global require dealerdirect/phpcodesniffer-composer-installer
RUN ln -s ~/.composer/vendor/bin/phpcs /usr/local/bin
RUN phpcs --config-set installed_paths ~/.composer/vendor/drupal/coder/coder_sniffer

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["sh"]
