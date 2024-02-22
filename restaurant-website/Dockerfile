FROM php:8.3-fpm-alpine

WORKDIR /var/www/html

RUN apk add icu-dev git && \
	docker-php-ext-configure intl && \
	docker-php-ext-install intl

COPY --chown=www-data:www-data . .


COPY --from=composer:lts /usr/bin/composer /usr/bin/composer
USER www-data
RUN composer install --optimize-autoloader

RUN php bin/console asset-map:compile && \
	php bin/console cache:clear --env=prod
