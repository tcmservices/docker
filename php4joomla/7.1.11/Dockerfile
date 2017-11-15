FROM php:7.1.11-apache

#Get latest package list
RUN apt-get update

#Install Linux Utils
RUN apt-get install -y apt-utils

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

WORKDIR /var/www/html

#/Install wget, needed to install composer
RUN apt-get install -y wget

#Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if ((hash_file('SHA384', 'composer-setup.php')) === (exec('wget -q -O - https://composer.github.io/installer.sig'))) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"

#Install man to be able to see the manual for commands
RUN apt-get install -y man

#Install Linux zip
RUN apt-get install -y zip

#COPY joomla_install.php /var/www/html/joomla_install.php
#RUN chown www-data:www-data joomla_install.php
#CMD [ "php", "/var/www/html/joomla_install.php" ]
#CMD [ "wget", "https://downloads.joomla.org/cms/joomla3/3-8-1/joomla_3-8-1-stable-full_package-zip" ]