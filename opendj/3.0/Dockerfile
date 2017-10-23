# Customized from https://github.com/ghchinoy/forgerock-docker
FROM davimss/openjdk-alpine:8
MAINTAINER DaviMSS <davimss@gmail.com>

WORKDIR /opt

ENV INSTALLPROP opendj-install.properties
ENV OPENDJ_FILE OpenDJ-3.0.0.zip

COPY imp.ldif /opt/imp.ldif
COPY $INSTALLPROP /opt/$INSTALLPROP

USER root

RUN set -x ; \
    apk add --no-cache --virtual .tmp-deps curl ; \
    curl -o /opt/$OPENDJ_FILE -L https://www.dropbox.com/s/70s0pscffpvtz93/$OPENDJ_FILE?dl=1 ; \
    unzip /opt/$OPENDJ_FILE ; \
    rm -f /opt/$OPENDJ_FILE ; \
    apk del .tmp-deps ; \
    apk del curl ; \
    rm -rf /var/cache/apk/* ; \
    chown -Rf caos:caos /opt/*

USER caos    

WORKDIR /opt/opendj

RUN ./setup --cli --propertiesFilePath /opt/$INSTALLPROP --acceptLicense --no-prompt

RUN ./bin/status

EXPOSE 4444 1389 1636

CMD ["/opt/opendj/bin/start-ds", "-N"]

# To build the image
#   docker build -t opendj .

# To run the container
#   docker run -d -p 1389:1389 -p 1636:1636 -p 4444:4444 --name opendj opendj