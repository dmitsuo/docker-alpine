FROM alpine:3.6
MAINTAINER DaviMSS <davimss@gmail.com>

RUN addgroup -S caos && adduser -D -S -G caos caos

RUN set -x ; \
    mkdir /opt ; \
    chmod 755 /opt ; \
    chown caos:caos -R /opt

WORKDIR /opt

# Specify the user which should be used to execute all commands below
USER caos

CMD /bin/sh