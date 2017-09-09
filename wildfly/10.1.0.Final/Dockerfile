FROM openjdk:8-jdk-alpine

USER root

ENV WILDFLY_VERSION 10.1.0.Final
ENV WILDFLY_HOME /opt/wf
ENV JBOSS_HOME $WILDFLY_HOME
ENV PATH $WILDFLY_HOME/bin:$PATH
ENV WILDFLY_DOWN_FILE wildfly-$WILDFLY_VERSION.tar.gz
#ENV CONFIG_FILE standalone-full.xml
ENV CONFIG_FILE standalone.xml

# RUN mkdir -p "$WILDFLY_HOME"

# WORKDIR $WILDFLY_HOME

#COPY $WILDFLY_DOWN_FILE $WILDFLY_HOME/$WILDFLY_DOWN_FILE

RUN set -x ; \
    mkdir -p $WILDFLY_HOME ; \
    cd $WILDFLY_HOME ; \
    #apk add --no-cache --virtual .tmp-deps curl ; \
    #curl -O http://download.jboss.org/wildfly/$WILDFLY_VERSION/$WILDFLY_DOWN_FILE ; \
    wget http://download.jboss.org/wildfly/$WILDFLY_VERSION/$WILDFLY_DOWN_FILE ; \
    tar -xvf $WILDFLY_DOWN_FILE --strip-components=1 ; \
    rm -rf bin/*.bat ; \
    rm -rf bin/*.ps1 ; \
    rm -rf $WILDFLY_DOWN_FILE ; \
    #apk del .tmp-deps ; \
    #apk del curl ; \
    #rm -rf /var/cache/apk/* ; \
    chown root:root -R /opt
# sh removes env vars it doesn't support (ones with periods)
# https://github.com/docker-library/tomcat/issues/77    
    #apk add --no-cache bash ; \
	#find ./bin/ -name '*.sh' -exec sed -ri 's|^#!/bin/sh$|#!/usr/bin/env bash|' '{}' +

WORKDIR $WILDFLY_HOME

#COPY $CONFIG_FILE standalone/configuration/$CONFIG_FILE
COPY standalone.conf bin/standalone.conf

EXPOSE 8080 9990

CMD bin/standalone.sh --server-config=$CONFIG_FILE -b 0.0.0.0