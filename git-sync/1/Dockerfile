# https://hub.docker.com/_/centos/
FROM centos:7
MAINTAINER billypon

# init
RUN cp -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# install
RUN yum install -y git crontabs

# clean
RUN yum autoremove -y
RUN yum clean all

# script
ADD git-sync /bin/

# cron
RUN touch /var/log/cron.log

VOLUME ["/git"]
CMD crond && tail -f /var/log/cron.log
