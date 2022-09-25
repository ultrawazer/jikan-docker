FROM php:8.1-apache-buster

ENV	COMPOSER_ALLOW_SUPERUSER 1

RUN	apt-get update && apt-get install -y \
	openssl \
	git \
	unzip \
	&& curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
	&& composer --version
	

RUN apt-get update -y && apt-get upgrade -y && apt-get install git libssl-dev -y
RUN pecl install mongodb && docker-php-ext-enable mongodb
RUN echo "extension=mongodb.so" >> /usr/local/etc/php/php.ini
	
RUN	git clone --branch=master --depth=1 https://github.com/jikan-me/jikan-rest.git . \
    && composer require 'composer/package-versions-deprecated:*' \
	&& composer install --prefer-dist --no-progress --classmap-authoritative  --no-interaction \
	&& composer update jikan-me/jikan

ADD	.env /run-jikan.sh ./

ENTRYPOINT ["./run-jikan.sh"]