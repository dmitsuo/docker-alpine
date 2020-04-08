FROM davimss/openjdk-alpine:8

ENV TOMCAT_MAJOR 9
ENV TOMCAT_VERSION 9.0.33
ENV TOMCAT_DIR apache-tomcat-$TOMCAT_VERSION
ENV TOMCAT_DOWN_FILE $TOMCAT_DIR.tar.gz
ENV CATALINA_HOME /opt/$TOMCAT_DIR
ENV PATH $CATALINA_HOME/bin:$PATH
ENV TOMCAT_DOWNLOAD_URL http://archive.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/$TOMCAT_DOWN_FILE
ENV TOMCAT_CONF_DIR ${CATALINA_HOME}/conf
ENV TOMCAT_BIN_DIR ${CATALINA_HOME}/bin
ENV TOMCAT_DEPLOY_DIR ${CATALINA_HOME}/webapps

USER root

RUN set -x ; \
    curl -jkSL -o /tmp/apache-tomcat.tar.gz http://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR}/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz ; \
    gunzip /tmp/apache-tomcat.tar.gz ; \
    tar -C /opt -xf /tmp/apache-tomcat.tar ; \
    ln -s $CATALINA_HOME /opt/tomcat ; \
    apk del curl && rm -rf /tmp/* /var/cache/apk/* ; \
    chown -R caos:caos /opt

USER caos

WORKDIR $CATALINA_HOME

CMD ["catalina.sh", "run"]