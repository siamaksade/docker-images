#######################################################################
#                                                                     #
# Creates a image with Sonatype nexus       						  #
#                                                                     #
#######################################################################

FROM siamaksade/base

MAINTAINER Siamak Sadeghianfar <ssadeghi@redhat.com>

USER root

RUN mkdir -p /opt/sonatype-nexus /opt/sonatype-work
RUN wget -O /tmp/nexus-bundle.tar.gz http://download.sonatype.com/nexus/oss/nexus-2.8.1-bundle.tar.gz
RUN tar xzvf /tmp/nexus-bundle.tar.gz -C /opt/sonatype-nexus --strip-components=1
RUN useradd --user-group --system --home-dir /opt/sonatype-nexus nexus

ADD nexus.xml /opt/sonatype-work/nexus/conf/nexus.xml

RUN chown -R nexus:nexus /opt/sonatype-work /opt/sonatype-nexus

ENV NEXUS_WEBAPP_CONTEXT_PATH /nexus
RUN echo "#!/bin/bash" > /opt/start-nexus.sh
RUN echo "su -c \"/opt/sonatype-nexus/bin/nexus console\" - nexus" >> /opt/start-nexus.sh
RUN chmod +x /opt/start-nexus.sh

CMD ["/opt/start-nexus.sh"]
EXPOSE 8081