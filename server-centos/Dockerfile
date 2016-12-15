# https://hub.docker.com/_/centos/
FROM centos:7
MAINTAINER billypon

RUN useradd -s /sbin/nologin -d /dev/null -M www -r -u 997 -g 997
RUN cp -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN ln -s service /sbin/start
RUN ln -s service /sbin/stop
RUN ln -s service /sbin/restart
RUN ln -s service /sbin/status

RUN yum install -y epel-release sudo
RUN yum install -y make gcc

# php
RUN yum install -y php php-fpm php-devel
RUN yum install -y php-bcmath php-gd php-json php-mbstring php-mcrypt php-xml php-xmlrpc php-soap
RUN yum install -y php-mysql php-pecl-redis
RUN yum install -y ImageMagick php-pecl-imagick sendmail

# php: eaccelerator
Add https://github.com/eaccelerator/eaccelerator/tarball/master /tmp/eaccelerator.tar.gz
RUN tar zxvf /tmp/eaccelerator.tar.gz -C /tmp
RUN cd /tmp/eaccelerator-* && phpize && ./configure && make && make install
RUN rm -rf /tmp/eaccelerator*

# php: zend guard loader
ADD http://downloads.zend.com/guard/6.0.0/ZendGuardLoader-70429-PHP-5.4-linux-glibc23-x86_64.tar.gz /tmp/ZendGuardLoader.tar.gz
RUN tar zxvf /tmp/ZendGuardLoader.tar.gz -C /tmp
RUN cd /tmp/ZendGuardLoader-*/php-* && cp ZendGuardLoader.so /usr/lib64/php/modules
RUN rm -rf /tmp/ZendGuardLoader*

# node
RUN curl --silent --location https://rpm.nodesource.com/setup_6.x | bash -
RUN yum install -y nodejs

# mono
RUN yum install -y yum-utils
RUN rpm --import "http://keyserver.ubuntu.com/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF"
RUN yum-config-manager --add-repo http://download.mono-project.com/repo/centos/
RUN yum install -y mono xsp

# redis
RUN yum install -y redis
RUN mkdir /home/redis
RUN chown redis:www /home/redis
RUN gpasswd -a redis www

# fix
RUN echo 'LC_ALL="POSIX"' >> /etc/locale.conf

# clean
RUN yum autoremove -y make gcc php-devel
RUN yum autoremove -y
RUN yum clean all

ENTRYPOINT ["/sbin/main"]
