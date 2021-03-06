# https://hub.docker.com/_/centos/
FROM centos:7
MAINTAINER billypon

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

# php: zend guard loader
ADD http://downloads.zend.com/guard/6.0.0/ZendGuardLoader-70429-PHP-5.4-linux-glibc23-x86_64.tar.gz /tmp/ZendGuardLoader.tar.gz
RUN tar zxvf /tmp/ZendGuardLoader.tar.gz -C /tmp
RUN cd /tmp/ZendGuardLoader-*/php-* && cp ZendGuardLoader.so /usr/lib64/php/modules

# redis
RUN yum install -y redis

# node
RUN curl --silent --location https://rpm.nodesource.com/setup_6.x | bash -
RUN yum install -y nodejs

# dotnet(/usr/lib/dotnet)

# mono
RUN yum install -y yum-utils
RUN rpm --import "http://keyserver.ubuntu.com/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF"
RUN yum-config-manager --add-repo http://download.mono-project.com/repo/centos/
RUN yum install -y mono xsp

# system
RUN cp -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN useradd -s /sbin/nologin -d /dev/null -M www
RUN sed -i "/PrivateTmp/d" /usr/lib/systemd/system/php-fpm.service
RUN rm -f /etc/systemd/system/multi-user.target.wants/{sendmail,sm-client}.service
RUN for x in `echo init php-fpm redis`; do ln -s /usr/lib/systemd/system/${x}.service /etc/systemd/system/multi-user.target.wants/; done

# fix
RUN echo 'LC_ALL="POSIX"' >> /etc/locale.conf

# clean
RUN yum autoremove -y make gcc php-devel
RUN yum autoremove -y
RUN yum clean all
RUN rm -rf /tmp/*

ENTRYPOINT ["/sbin/init"]
