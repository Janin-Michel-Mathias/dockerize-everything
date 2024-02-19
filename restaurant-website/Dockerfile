# Stage 1: Build Stage
FROM php:8.3-fpm

WORKDIR /var/www/html

COPY . .

ENV COMPOSER_ALLOW_SUPERUSER=1

RUN apt update
RUN apt install zip -y
RUN apt install -y libicu-dev git
RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'edb40769019ccf227279e3bdd1f5b2e9950eb000c3233ee85148944e555d97be3ea4f40c3c2fe73b22f875385f6a5155') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
RUN php bin/console asset-map:compile
RUN php bin/console cache:clear --env=prod
RUN composer install --no-dev --optimize-autoloader
RUN chmod -R 777 ./**/*