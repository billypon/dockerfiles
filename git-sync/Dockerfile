FROM billypon/alpine:3.5
MAINTAINER billypon

RUN apk add --no-cache openssh-client git
ADD git-sync /bin/

WORKDIR /home/git
VOLUME ["/home/git"]
ENTRYPOINT ["git-sync", "-dc"]
