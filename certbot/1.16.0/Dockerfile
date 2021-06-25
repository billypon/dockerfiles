FROM certbot/certbot:v1.16.0
MAINTAINER billypon

ADD certbot /certbot

RUN apk add --no-cache grep curl jq && \
	ln -s /certbot/certonly /usr/local/bin && \
	ln -s /dev/null /var/log/certbot

WORKDIR /certbot
ENTRYPOINT [ "/certbot/entrypoint" ]
