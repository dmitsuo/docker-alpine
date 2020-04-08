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
    rm -rf $CATALINA_HOME/webapps/* ; \
    apk del curl && rm -rf /tmp/* /var/cache/apk/* ; \
    cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1 > /tmp/myfile    ; \
    ${JAVA_HOME}/bin/keytool -genkeypair -alias tomcat -keyalg RSA -keysize 2048      \
    -storetype PKCS12 -keystore ${TOMCAT_CONF_DIR}/tomcat-keystore.p12 -validity 3650   \
    -dname "cn=myappserver,ou=mydept,o=mycompany,l=mycity,s=ss,c=cc"                  \
    -keypass $(cat /tmp/myfile) -storepass $(cat /tmp/myfile)                       ; \
    sed -i "71s|.*|redirectPort=\"8443\" compression=\"on\" compressionMinSize=\"128\" compressibleMimeType=\"application/json,text/html,text/xml,application/xml,application/xhtml+xml,text/javascript,text/css,text/plain,text/csv,text/rtf,application/x-javascript,application/javascript,image/svg+xml\"/>|" $TOMCAT_CONF_DIR/server.xml ; \
    sed -i "114s|.*|<Connector port=\"8443\" protocol=\"org.apache.coyote.http11.Http11NioProtocol\" maxThreads=\"200\" SSLEnabled=\"true\" scheme=\"https\" secure=\"true\" keystoreFile=\"${TOMCAT_CONF_DIR}/tomcat-keystore.p12\" keystorePass=\"$(cat /tmp/myfile)\" clientAuth=\"false\" sslProtocol=\"TLS\" compression=\"on\" compressionMinSize=\"128\" compressibleMimeType=\"application/json,text/html,text/xml,application/xml,application/xhtml+xml,text/javascript,text/css,text/plain,text/csv,text/rtf,application/x-javascript,application/javascript,image/svg+xml\" />|" $TOMCAT_CONF_DIR/server.xml ; \
    echo $'\nexport JAVA_OPTS="$JAVA_OPTS -Duser.language=pt -Duser.country=BR -Duser.timezone=America/Belem"' >> ${TOMCAT_BIN_DIR}/setenv.sh ; \
    echo $'\njava.util.logging.SimpleFormatter.format=%1$tF %1$tT [%4$s][%2$s] %5$s %6$s %n' >> ${TOMCAT_CONF_DIR}/logging.properties ; \
    chown -R caos:caos /opt ; \
    rm -f /tmp/myfile

USER caos

WORKDIR $CATALINA_HOME

CMD ["catalina.sh", "run"]