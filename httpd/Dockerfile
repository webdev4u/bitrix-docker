FROM php:7.2-apache

# provision with configs
ADD conf/modules.conf /etc/apache2/conf-enabled/
ADD conf/server.conf /etc/apache2/sites-enabled/
ADD conf/bitrixenv.ini /usr/local/etc/php/conf.d/

# enable remoteip module
RUN ln -s /etc/apache2/mods-available/remoteip.load /etc/apache2/mods-enabled/remoteip.load

# update system
RUN apt-get update > /dev/null \ 
    &&  apt-get install -qy libzip-dev libldb-dev libldap2-dev libmcrypt-dev libpng-dev libjpeg62-turbo-dev libfreetype6-dev \
    && apt-get clean > /dev/null

# install GD
RUN     docker-php-ext-configure gd \
        --with-jpeg-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-freetype-dir=/usr/include/ \
    &&  docker-php-ext-install gd > /dev/null

# install other Exts
RUN    docker-php-ext-configure zip --with-libzip > /dev/null \
    && docker-php-ext-install zip > /dev/null \
    &&  docker-php-ext-install ldap > /dev/null \
    &&  docker-php-ext-install opcache > /dev/null \
    &&  docker-php-ext-install xml > /dev/null \
    &&  docker-php-ext-install xmlreader > /dev/null \
    &&  docker-php-ext-install xmlwriter > /dev/null \
    &&  docker-php-ext-install xmlrpc > /dev/null \
    &&  docker-php-ext-install bz2 > /dev/null \
    &&  docker-php-ext-install xdebug > /dev/null \
    &&  docker-php-ext-install calendar > /dev/null \
    &&  docker-php-ext-install ctype > /dev/null \
    &&  docker-php-ext-install curl > /dev/null \
    &&  docker-php-ext-install mbstring > /dev/null \
    &&  docker-php-ext-install dom > /dev/null \
    &&  docker-php-ext-install json > /dev/null \
    &&  docker-php-ext-install mysqli > /dev/null

# change container uid according to host user
RUN usermod -u 1000 www-data

CMD /usr/sbin/apache2ctl -D FOREGROUND