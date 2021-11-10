FROM alpine:3.14.2
MAINTAINER billypon

RUN apk add --no-cache syncthing && mkdir -p ~/.config

WORKDIR /home/syncthing
EXPOSE 8384 22000 21027/udp
VOLUME [ "/home/syncthing", "/root/.config/syncthing" ]
CMD [ "syncthing", "-logflags=3" ]
