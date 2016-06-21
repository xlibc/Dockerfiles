#
# Dockerfile for shadowsocks-libev
#

FROM alpine:latest
MAINTAINER Samuel X. S. Zeng <i@xlibc.me>

ENV SS_VER v2.4.7
ENV SS_URL https://github.com/shadowsocks/shadowsocks-libev/archive/$SS_VER.tar.gz
ENV SS_DIR shadowsocks-libev-$SS_VER
ENV SS_DEP autoconf build-base curl libtool linux-headers openssl-dev

RUN set -ex \
    && apk add --update $SS_DEP \
    && curl -sSL $SS_URL | tar xz \
    && cd $SS_DIR \
        && ./configure \
        && make install \
        && cd .. \
        && rm -rf $SS_DIR \
    && apk del --purge $SS_DEP \
    && rm -rf /var/cache/apk/*

ENV SERVER_PORT 38388

EXPOSE $SERVER_PORT/tcp
EXPOSE $SERVER_PORT/udp

ENTRYPOINT ["ss-server"]
