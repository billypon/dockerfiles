FROM alpine:3.7
MAINTAINER billypon

RUN apk add --no-cache darkhttpd && \
    wget https://github.com/ziahamza/webui-aria2/archive/master.zip && \
    unzip -x master.zip && \
    rm master.zip && \
    mv webui-aria2-master webui-aria2 && \
    sleep 0

WORKDIR /webui-aria2
EXPOSE 8888
CMD ["darkhttpd", "/webui-aria2", "--port", "8888"]
