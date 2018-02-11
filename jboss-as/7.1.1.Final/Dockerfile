FROM davimss/openjdk-alpine:7

ENV JBOSS_VERSION jboss-as-7.1.1.Final
ENV JBOSS_ZIP $JBOSS_VERSION.zip
ENV JBOSS_HOME /opt/$JBOSS_VERSION

USER root

#COPY $JBOSS_ZIP /opt/

RUN set -x ; \
    apk add --no-cache --virtual .tmp-deps curl ; \
    curl -o /opt/$JBOSS_ZIP -L https://www.dropbox.com/s/jm98r1u7dktz7yu/$JBOSS_ZIP?dl=1 ; \
    unzip /opt/$JBOSS_ZIP ; \
    rm -f /opt/$JBOSS_ZIP ; \
    apk del .tmp-deps ; \
    apk del curl ; \
    rm -rf /var/cache/apk/* ; \
    ln -s $JBOSS_HOME /opt/jboss ; \
    echo -e "\nJAVA_OPTS=\"\$JAVA_OPTS -Duser.language=pt -Duser.country=BR -Duser.timezone=America/Belem\"\n" >> $JBOSS_HOME/bin/standalone.conf ; \
    chown -Rf caos:caos /opt/*

USER caos

EXPOSE 8080 9990

CMD $JBOSS_HOME/bin/standalone.sh -b=0.0.0.0 -bmanagement=0.0.0.0