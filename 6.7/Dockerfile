FROM alpine:3.20.2 as build

ENV NAME=squid \
    VERSION=6.7\
    DOWNLOAD_URL=http://www.squid-cache.org/Versions/v6/squid-6.7.tar.gz

RUN apk update --no-cache && \
    apk add curl build-base openssl-dev perl-dev autoconf automake heimdal-dev libtool libcap-dev linux-headers && \
    curl -sSL $DOWNLOAD_URL -o squid.tar.gz && \
    tar xzf squid.tar.gz && \
    cd $NAME-$VERSION/ && \
    ./configure \
      --prefix=/opt/squid \
      --disable-strict-error-checking \
      --disable-arch-native \
      --enable-delay-pools \
      --enable-linux-netfilter \
      --enable-auth \
      --with-openssl && \
    make && \
    make install

FROM alpine:3.20.2

COPY --from=build /opt/squid /opt/squid
WORKDIR /opt/squid/

RUN apk add --no-cache libcap libltdl libstdc++ libgcc && \
    addgroup -g 1000 _squid && adduser -D -H -G _squid -u 1000 -S _squid && \
    chown _squid:_squid -R /opt/squid

USER _squid

EXPOSE 3128/tcp

ENTRYPOINT [ "/opt/squid/sbin/squid" ]

CMD  [ "-N", "-d1", "-f", "/opt/squid/etc/squid.conf" ]
