FROM php:7.2.7-apache

#Get latest package list
RUN apt-get update && apt-get install -y \
	#Install Linux Utils
	apt-utils \
	#Install Vim editor
    vim \
	#Install mcrypt support
    libmcrypt-dev \
    libreadline-dev \
    #Install Linux zip
    libzip-dev zip \
    #/Install wget, needed to install composer
    wget \
    #Install man to be able to see the manual for commands
    man \
   	#Install GD
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    #Install Soap dependency
    libxml2-dev \
    #Install Cron
    cron \
    #Install mysql client
    mysql-client

#Install mcrypt support
RUN pecl install mcrypt-1.0.1

#Install and enable native ZIP support for PHP
RUN pecl install zip && docker-php-ext-enable zip

#Install xdebug support
RUN pecl install xdebug && docker-php-ext-enable xdebug

#Install & Enable GD in PHP
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/ --with-jpeg-dir=/usr/ --with-png-dir=/usr/ && docker-php-ext-install gd

#Install mysqli support
RUN	docker-php-ext-install mysqli

#Configure xdebug
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_host=10.0.75.1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

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

#Install some needed packages to use add-apt-repository
#RUN apt-get install -y software-properties-common python-software-properties

#Install Soap
RUN docker-php-ext-install soap

#Install PDO MYSQL
RUN docker-php-ext-install pdo_mysql

#Rename php extensions directory
RUN mv /usr/local/lib/php/extensions/no-debug-non-zts-20170718/* /usr/local/lib/php/extensions

#add a default php.ini file
RUN echo "extension_dir=/usr/local/lib/php/extensions" >> /usr/local/etc/php/php.ini
