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

MAINTAINER Giorgos Argyriou <gioargyr@gmail.com>

RUN apt-get update \
 && apt-get install -y mercurial \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN hg clone 'http://hg.strabon.di.uoa.gr/Strabon/' \
 && sed -i 's/localhost/postgis/' /Strabon/endpoint/WebContent/WEB-INF/connection.properties \
 && cd Strabon \
 && mvn clean package

RUN mkdir /resources \
 && cp /Strabon/endpoint/target/strabon-endpoint-3.3.2-SNAPSHOT.war /tomcat/webapps/strabon.war

CMD ["/bin/bash", "/runtomcat.sh"]