FROM davimss/openjdk-alpine:8

ENV JBOSS_ZIP jboss-eap-6.4-CVE-2015-7501.zip
ENV JBOSS_HOME /opt/jboss-eap-6.4

USER root

#COPY $JBOSS_ZIP /opt/

RUN set -x ; \
    apk add --no-cache --virtual .tmp-deps curl ; \
    curl -o /opt/$JBOSS_ZIP -L https://www.dropbox.com/s/zmv8och1s78ibmp/$JBOSS_ZIP?dl=1 ; \
    unzip /opt/$JBOSS_ZIP ; \
    rm -f /opt/$JBOSS_ZIP ; \
    apk del .tmp-deps ; \
    apk del curl ; \
    rm -rf /var/cache/apk/* ; \
    chown -Rf caos:caos /opt/*

USER caos

COPY standalone.conf $JBOSS_HOME/bin/

EXPOSE 8080 9990

CMD $JBOSS_HOME/bin/standalone.sh -b=0.0.0.0 -bmanagement=0.0.0.0