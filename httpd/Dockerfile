FROM php:7.2-apache

# provision with configs
COPY ./conf/modules.conf /etc/apache2/conf-enabled/modules.conf
COPY ./conf/server.conf /etc/apache2/sites-enabled/server.conf
COPY ./conf/bitrixenv.ini /usr/local/etc/php/conf.d/bitrixenv.ini

# enable remoteip module
RUN ln -s /etc/apache2/mods-available/remoteip.load /etc/apache2/mods-enabled/remoteip.load

# update system
RUN apt-get update > /dev/null \ 
    &&  apt-get install -qy libzip-dev libbz2-dev libldb-dev libldap2-dev libmcrypt-dev libpng-dev libjpeg62-turbo-dev libfreetype6-dev mailutils \
    && apt-get clean > /dev/null

# install GD
RUN     docker-php-ext-configure gd \
        --with-jpeg-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-freetype-dir=/usr/include/ \
    &&  docker-php-ext-install gd

# install other Exts
RUN    docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install zip \
    &&  docker-php-ext-install ldap \
    &&  docker-php-ext-install opcache \
    # &&  docker-php-ext-configure xmlrpc --with-libxml2 \
    # &&  docker-php-ext-install xmlrpc \
    &&  docker-php-ext-install bz2 \
    &&  docker-php-ext-install calendar \
    &&  docker-php-ext-install mysqli
RUN pecl install xdebug && docker-php-ext-enable xdebug
# change container uid according to host user
RUN usermod -u 1000 www-data

CMD /usr/sbin/apache2ctl -D FOREGROUND