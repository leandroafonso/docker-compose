FROM ubuntu:latest
MAINTAINER leandroafonso<leandro@leandroafonso.com>
ENV DEBIAN_FRONTEND noninteractive

# Install basics
RUN apt-get update
RUN apt-get install -y vim
RUN apt-get install -y curl zip unzip git software-properties-common
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
RUN apt-get update
RUN echo "\n10.30.0.2	801f3fde25f1 api.newenv.myeggs.com.br newenv.myeggs.com.br" > /etc/hosts
# Install PHP 5.6
RUN apt-get install -y php5.6 php5.6-mysql php5.6-mcrypt php5.6-cli php5.6-gd php5.6-curl php5.6-mbstring php5.6-xml php5.6-redis php5.6-mongo php5.6-xdebug

ADD php-config/php-apache2.ini /etc/php/5.6/apache2/php.ini
ADD php-config/php-cli.ini /etc/php/5.6/cli/php.ini
ADD php-config/20-xdebug.ini /etc/php/5.6/apache2/conf.d/20-xdebug.ini
ADD php-config/20-xdebug.ini /etc/php/5.6/cli/conf.d/20-xdebug.ini


# Enable apache mods.
RUN a2enmod php5.6
RUN a2enmod rewrite

#update php.ini set error log path
RUN mkdir /var/log/php

ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
# Expose apache.
#EXPOSE 80
#EXPOSE 9001
#EXPOSE 443
#EXPOSE 9091
# Update the default apache site with the config we created.
RUN mkdir /var/www/local.app
RUN mkdir /var/www/local.app/public_html
ADD apache-config.conf /etc/apache2/sites-enabled/000-default.conf
# By default start up apache in the foreground, override with /bin/bash for interative.
CMD /usr/sbin/apache2ctl -D FOREGROUND
