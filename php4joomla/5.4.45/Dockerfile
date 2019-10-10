FROM php:5.4-apache

#Get latest package list
RUN apt-get update && apt-get install -y \
	#Install Linux Utils
	apt-utils \
	#Install Vim editor
	vim \
	#Install mcrypt support
	libmcrypt-dev \
	#Install native ZIP support
	libzip-dev \
	#/Install wget, needed to install composer
    wget \
	#Install man to be able to see the manual for commands
	man \
	#Install Linux zip
	zip \
	#Install some needed packages to use add-apt-repository
	software-properties-common \
	python-software-properties \
	#Install GD
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libpng12-dev \
 	#Install Soap
 	libxml2-dev \
 	#Install Cron
    cron \
	#install mysql client
	mysql-client

#Install GD
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/ --with-jpeg-dir=/usr/ --with-png-dir=/usr/ && docker-php-ext-install gd

#Install mcrypt support
RUN	docker-php-ext-install mcrypt

#Install mysqli support
RUN	docker-php-ext-install mysqli

#Install native ZIP support
RUN pecl install zip && docker-php-ext-enable zip

WORKDIR /var/www/html

#Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if ((hash_file('SHA384', 'composer-setup.php')) === (exec('wget -q -O - https://composer.github.io/installer.sig'))) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"

#Enable Mod_Rewrite
RUN a2enmod rewrite

#Install BC Math
RUN	docker-php-ext-install bcmath

#Install Soap
RUN docker-php-ext-install soap

#Install PDO MYSQL
RUN docker-php-ext-install pdo_mysql

#Rename php extensions directory
RUN mv /usr/local/lib/php/extensions/no-debug-non-zts-20100525/* /usr/local/lib/php/extensions

#add a default php.ini file
RUN echo "extension_dir=/usr/local/lib/php/extensions" >> /usr/local/etc/php/php.ini

#Add custom php.ini
#ADD php.ini /usr/local/etc/php

#COPY joomla_install.php /var/www/html/joomla_install.php
#RUN chown www-data:www-data joomla_install.php
#CMD [ "php", "/var/www/html/joomla_install.php" ]
#CMD [ "wget", "https://downloads.joomla.org/cms/joomla3/3-8-1/joomla_3-8-1-stable-full_package-zip" ]
