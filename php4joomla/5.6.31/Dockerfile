FROM php:5.6.31-apache

#Get latest package list
RUN apt-get update

#Install Vim editor
RUN apt-get install -y vim

#Install mcrypt support
RUN	apt-get install -y libmcrypt-dev && docker-php-ext-install mcrypt

#Install mysqli support
RUN	docker-php-ext-install mysqli

#Install native ZIP support
RUN apt-get install -y libzip-dev && pecl install zip && docker-php-ext-enable zip

#Install xdebug support
RUN pecl install xdebug && docker-php-ext-enable xdebug

#Configure xdebug
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_host=10.0.75.1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini