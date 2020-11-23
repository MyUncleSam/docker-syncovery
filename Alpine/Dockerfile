# NOT SUPPORTED!

FROM alpine:latest
#FROM frolvlad/alpine-glibc

ENV SYNCOVERY_HOME=/config
ENV SETUP_TEMP=/tmp/syncovery.tar.gz

RUN mkdir -p /docker /syncovery /tmp /config
ADD ./docker-entrypoint.sh /docker/entrypoint.sh

RUN apk update
RUN apk add bash wget openssl libressl-dev zlib zlib-dev sqlite sqlite-libs libcrypto1.1 libsmbclient

RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub
RUN wget -q -O /tmp/glibc.apk https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.31-r0/glibc-2.31-r0.apk
RUN wget -q -O /tmp/glibc-bin.apk https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.31-r0/glibc-bin-2.31-r0.apk
RUN wget -q -O /tmp/glibc-dev.apk https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.31-r0/glibc-dev-2.31-r0.apk
RUN wget -q -O /tmp/glibc-i18n.apk https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.31-r0/glibc-i18n-2.31-r0.apk

RUN apk add /tmp/glibc.apk /tmp/glibc-bin.apk /tmp/glibc-dev.apk /tmp/glibc-i18n.apk
RUN rm -R /tmp/*

ENV LD_LIBRARY_PATH=/lib:/usr/local/lib:/usr/bin
RUN export LD_LIBRARY_PATH

RUN wget -O "$SETUP_TEMP" 'https://www.syncovery.com/release/SyncoveryCL-x86_64-9.21-Web.tar.gz'
RUN tar -xvf "$SETUP_TEMP" --directory /syncovery
RUN rm -f "$SETUP_TEMP"

RUN chmod +x /syncovery/SyncoveryCL
RUN chmod +x /docker/entrypoint.sh

EXPOSE 8999

ENTRYPOINT [ "/docker/entrypoint.sh" ]