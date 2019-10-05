FROM nginx:stable

ADD conf/nginx.conf /etc/nginx/
ADD conf/host.conf /etc/nginx/conf.d/

RUN usermod -u 1000 www-data

EXPOSE 80 443
