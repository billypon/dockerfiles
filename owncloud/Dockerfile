# https://hub.docker.com/_/centos/
FROM centos:7
MAINTAINER billypon

# init
RUN cp -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# install
RUN yum install -y owncloud-nginx redis php-redis

# clean
RUN yum autoremove -y
RUN yum clean all

# nginx
ADD nginx/nginx.conf /etc/nginx/
RUN rm -rf /etc/nginx/conf.d/
ADD nginx/conf.d/ /etc/nginx/

# php-fpm
RUN rm -rf /etc/php-fpm.d/
ADD php-fpm.d/ /etc/

# owncloud
RUN mkdir -p /var/lib/php/session
chown root.root -R /etc/owncloud/ /var/lib/owncloud/ /var/lib/php/session

CMD /bin/bash
