FROM alpine:3.5
MAINTAINER billypon

ADD localtime /etc/localtime
RUN apk add --no-cache openssh-client git
ADD git-sync /bin/

WORKDIR /home/git
VOLUME ["/home/git"]
CMD ["git-sync", "-dc"]
