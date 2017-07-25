FROM ubuntu:16.10

MAINTAINER KENICHI NAITO

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update

RUN apt-get install -y apt-utils

RUN apt-get install -y build-essential

RUN apt-get install -y debconf-utils

RUN apt-get install -y mysql-server mysql-client libmysqlclient-dev

RUN apt-get install -y apache2

RUN apt-get install -y imagemagick

RUN apt-get install -y postfix

RUN apt-get install -y vim

RUN apt-get install -y php libapache2-mod-php php-mcrypt php-zip php-mbstring php-xml phpunit

RUN apt-get install -y zip unzip
RUN phpenmod mcrypt

RUN apt-get install -y curl

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN useradd -ms /bin/bash laravel

COPY files/000-default.conf /etc/apache2/sites-available/000-default.conf

USER laravel

RUN mkdir /home/laravel/work

COPY files/bash_profile.txt /home/laravel/.bash_profile

USER root
ENTRYPOINT service apache2 start && service mysql start && service postfix start && bash
