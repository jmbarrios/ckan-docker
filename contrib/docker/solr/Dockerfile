####
#
# Dockerfile for building a Apache Solr;
#
# with scope to ckan
#
####
FROM eccenca/baseimage:1.0.1
MAINTAINER Henri Knochenhauer <henri.knochenhauer@eccenca.com>
MAINTAINER René Pietzsch <rene.pietzsch@eccenca.com>


#set env
ENV DEBIAN_FRONTEND noninteractive

# Install Java
RUN apt-get -q -y update && \
    apt-get -q -y install default-jre-headless

# Install Solr
ENV SOLR_HOME /opt/solr/example/solr
ENV SOLR_VERSION 4.10.2
ENV SOLR solr-$SOLR_VERSION
ENV CKAN_VERSION 2.2.1

RUN mkdir -p /opt/solr
ADD http://ftp-stud.hs-esslingen.de/pub/Mirrors/ftp.apache.org/dist/lucene/solr/$SOLR_VERSION/$SOLR.tgz /opt/$SOLR.tgz
RUN tar zxf /opt/$SOLR.tgz -C /opt/solr --strip-components 1

# Install CKAN Solr core
RUN cp -R $SOLR_HOME/collection1/ $SOLR_HOME/ckan/
RUN echo name=ckan > $SOLR_HOME/ckan/core.properties
#ADD schema.xml $SOLR_HOME/ckan/conf/schema.xml
ADD https://github.com/ckan/ckan/raw/ckan-$CKAN_VERSION/ckan/config/solr/schema.xml $SOLR_HOME/ckan/conf/schema.xml

EXPOSE 8983
WORKDIR /opt/solr/example
CMD ["java", "-jar", "start.jar"]
