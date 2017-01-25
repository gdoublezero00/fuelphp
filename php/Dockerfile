FROM php:7-apache

#COPY Oracle InstantClient
#ADD instantclient_12_1.tar.bz2 /usr/local/
#ENV ORACLE_HOME=/usr/local/instantclient_12_1 \
#	NLS_LANG=Japanese_Japan.AL32UTF8
#RUN ln -s /usr/local/instantclient_12_1/libclntsh.so.12.1 /usr/local/instantclient_12_1/libclntsh.so

#Package Install
RUN apt-get update &&  apt-get install -y libaio1 libmcrypt-dev freetds-dev libicu-dev libpq-dev libsqlite3-dev libssl-dev libpng-dev  zlib1g-dev \
	&& cp -s /usr/lib/x86_64-linux-gnu/libsybdb.so /usr/lib/

#RUN docker-php-ext-configure oci8 --with-oci8=instantclient,/usr/local/instantclient_12_1,12.1 \
	#&& docker-php-ext-configure pdo_oci --with-pdo-oci=instantclient,/usr/local/instantclient_12_1,12.1

#Redis
ENV PHPREDIS_VERSION 3.1.0
RUN curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz \
	&& tar xfz /tmp/redis.tar.gz \
	&& rm -r /tmp/redis.tar.gz \
	&& mv phpredis-$PHPREDIS_VERSION /usr/src/php/ext/redis 

#RUN docker-php-ext-install oci8 pdo_oci mbstring fileinfo mcrypt mysqli pdo_mysql redis pdo_dblib pdo_sqlite gd
RUN docker-php-ext-install mbstring fileinfo mcrypt mysqli pdo_mysql redis pdo_dblib pdo_sqlite gd

RUN a2enmod rewrite

RUN pecl install mongodb \
	&& echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/docker-php-ext-mongodb.ini

RUN service apache2 restart
