FROM openjdk:8u212-jdk-alpine3.9

RUN set -x ; \
    addgroup -S -g 1000 caos ; \
    adduser -S -u 1000 -s /sbin/nologin -D -h /opt -H -G caos caos ; \
    apk -U upgrade --update && apk add curl && apk add ttf-dejavu ; \
    chown -R caos:caos /opt

USER caos