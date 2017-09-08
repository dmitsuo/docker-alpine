FROM openjdk:7-jdk-alpine

USER root

ENV TOMCAT_MAJOR 7
ENV TOMCAT_VERSION 7.0.59
ENV TOMCAT_DIR apache-tomcat-$TOMCAT_VERSION
ENV TOMCAT_DOWN_FILE $TOMCAT_DIR.tar.gz
ENV CATALINA_HOME /opt/$TOMCAT_DIR
ENV PATH $CATALINA_HOME/bin:$PATH

ADD http://archive.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/$TOMCAT_DOWN_FILE /opt

WORKDIR $CATALINA_HOME
COPY setenv.sh bin/setenv.sh
#COPY server.xml conf/server.xml
COPY tomcat-users.xml conf/tomcat-users.xml
COPY logging.properties conf/logging.properties

# Estudar comando abaixo
VOLUME "$CATALINA_HOME/logs"

EXPOSE 8080

CMD ["catalina.sh", "run"]