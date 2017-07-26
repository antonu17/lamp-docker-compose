FROM php:7.0-apache
LABEL maintainer="antonu17@gmail.com"

COPY src/ /var/www/html/

# Enable Apache Rewrite Module
RUN a2enmod rewrite

# Install PHP extensions
RUN apt-get update \
  && apt-get install -y \
	  libpng12-dev \
		libjpeg-dev \
		libmcrypt-dev \
		zip \
		unzip \
	&& rm -rf /var/lib/apt/lists/* \
	&& docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
	&& docker-php-ext-install gd \
  && docker-php-ext-install mysqli \
  && docker-php-ext-install mcrypt \
  && docker-php-ext-install zip

RUN groupadd --gid 48 \
             apache \
  && useradd --uid 48 \
             --gid 48 \
             --no-create-home \
             --home-dir /var/www \
             --shell /usr/sbin/nologin \
             apache
