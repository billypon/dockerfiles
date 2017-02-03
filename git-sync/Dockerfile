FROM alpine:3.5
MAINTAINER billypon

RUN apk add --no-cache openssh-client git
ADD git-sync /bin/

VOLUME ["/home/git"]
CMD ["/bin/git-sync", "-d"]
