#######################################
# Dockerfile for Strabon              #
# BigDataEurope                       #
#                                     #
# based on bde2020/sc7pilotbase:1.0.0 #
# java 1.8.0_151                      #
# maven 3.0.5                         #
# git 1.9.1                           #
# tomcat 8.0.23                       #
#######################################
FROM bde2020/sc7pilotbase:1.0.0
ARG STRABON_VERSION
ARG STRABON_TAG="v$STRABON_VERSION"

LABEL maintainer='Giorgos Argyriou <gioargyr@gmail.com>'
LABEL authors='Giorgos Argyriou <gioargyr@gmail.com>, Aurelien Bourdon <aurelien.bourdon@gmail.com>'

RUN apt-get update \
 && apt-get install --assume-yes mercurial \
 && apt-get --assume-yes --purge autoremove \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN hg clone 'http://hg.strabon.di.uoa.gr/Strabon/' \
 && cd Strabon \
 && hg up $STRABON_TAG \
 && mvn package

ENV STRABON_HOME=/tomcat/webapps/strabon
RUN mkdir /resources \
 && unzip -d $STRABON_HOME /Strabon/endpoint/target/strabon-endpoint-$STRABON_VERSION.war

ADD entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/bin/bash", "/entrypoint.sh"]

CMD ["/bin/bash", "/runtomcat.sh"]