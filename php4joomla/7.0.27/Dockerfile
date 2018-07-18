FROM php:7.0.27-apache

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

#Enable Mod_Rewrite
RUN a2enmod rewrite

#Install BC Math
RUN	docker-php-ext-install bcmath

#Install some needed packages to use add-apt-repository
RUN apt-get install -y software-properties-common python-software-properties

#Install GD
RUN apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/ --with-jpeg-dir=/usr/ --with-png-dir=/usr/ \
    && docker-php-ext-install gd

#Install Soap
RUN apt-get install -y libxml2-dev && docker-php-ext-install soap


#Install PDO MYSQL
RUN docker-php-ext-install pdo_mysql

#Rename php extensions directory
RUN mv /usr/local/lib/php/extensions/no-debug-non-zts-20151012/* /usr/local/lib/php/extensions

#add a default php.ini file
RUN echo "extension_dir=/usr/local/lib/php/extensions" >> /usr/local/etc/php/php.ini

#Add custom php.ini
#COPY php.ini /usr/local/etc/php/

#COPY joomla_install.php /var/www/html/joomla_install.php
#RUN chown www-data:www-data joomla_install.php
#CMD [ "php", "/var/www/html/joomla_install.php" ]
#CMD [ "wget", "https://downloads.joomla.org/cms/joomla3/3-8-1/joomla_3-8-1-stable-full_package-zip" ]