FROM alpine:3.4

MAINTAINER Gavin Zhou <gavin.zhou@gmail.com>

ENV GOR_VERSION=0.15.1

RUN set -x \
 && addgroup pumba && adduser -s /bin/ash -D -G pumba pumba \
 && apk add --no-cache --virtual .gosu-deps dpkg gnupg openssl ca-certificates make gcc musl-dev curl \
 && curl -sSL https://github.com/Yelp/dumb-init/archive/master.tar.gz | tar -xz \
 && cd dumb-init-master && gcc -std=gnu99 -s -Wall -Werror -O3 -o /sbin/dumb-init /dumb-init-master/dumb-init.c \
 && cd /usr/local/bin \
 && curl -sSL https://github.com/buger/gor/releases/download/v${GOR_VERSION}/gor_v${GOR_VERSION}_x64.tar.gz| tar -xz \
 && apk del .gosu-deps

COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["gor", "--help"]
