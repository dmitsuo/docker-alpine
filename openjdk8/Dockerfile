FROM openjdk:8-jdk-alpine

RUN addgroup -g 1000 -S caos && adduser -u 1000 -D -S -G caos caos

RUN set -x ; \
    mkdir /opt ; \
    chmod 755 /opt ; \
    chown caos:caos -R /opt

WORKDIR /opt

# Specify the user which should be used to execute all commands below
USER caos

CMD /bin/sh