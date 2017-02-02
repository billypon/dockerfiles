# https://hub.docker.com/_/centos/
FROM centos:7
MAINTAINER billypon

RUN yum install -y git crontabs

# cron
RUN touch /var/log/cron.log

# system
RUN cp -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# clean
RUN yum autoremove -y
RUN yum clean all

CMD crond && tail -f /var/log/cron.log
