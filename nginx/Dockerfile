FROM nginx:stable

RUN sed -i -e 's/{{domain}}/${APP_DOMAIN}/g' conf/ssl_host.conf
ADD conf/nginx.conf /etc/nginx/
ADD conf/host.conf /etc/nginx/conf.d/
ADD conf/ssl_host.conf /etc/nginx/conf.d/

RUN usermod -u 1000 www-data

EXPOSE 80 443
