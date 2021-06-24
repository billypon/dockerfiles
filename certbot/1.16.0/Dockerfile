FROM certbot/certbot:v1.16.0
MAINTAINER billypon

ADD certbot /certbot

RUN apk add --no-cache grep curl jq

WORKDIR /certbot
ENTRYPOINT [ "/certbot/certbot" ]
