#######################################################################
#                                                                     #
# Creates a SonarQube image       							  		  #
#                                                                     #
#######################################################################

FROM siamaksade/base

MAINTAINER Siamak Sadeghianfar <ssadeghi@redhat.com>

USER root

############################################
# Install PostgreSQL
############################################

RUN yum -y localinstall http://yum.postgresql.org/9.3/redhat/rhel-6-x86_64/pgdg-centos93-9.3-1.noarch.rpm
RUN yum -y install postgresql93-server postgresql93
RUN /etc/init.d/postgresql-9.3 initdb
RUN sed -i "s/peer/trust/g" /var/lib/pgsql/9.3/data/pg_hba.conf
RUN sed -i "s/ident/md5/g" /var/lib/pgsql/9.3/data/pg_hba.conf
RUN echo "host    all             all             0.0.0.0/0               md5" >> /var/lib/pgsql/9.3/data/pg_hba.conf

RUN echo "listen_addresses='*'" >> /var/lib/pgsql/9.3/data/postgresql.conf
RUN /etc/init.d/postgresql-9.3 start && \
	psql -U postgres --command "CREATE USER sonar WITH SUPERUSER PASSWORD 'sonar';" && \
	runuser -l postgres -c "createdb -O sonar sonar"

############################################
# Install SonarQube
############################################

RUN wget -O /tmp/sonarqube-4.4.zip http://dist.sonar.codehaus.org/sonarqube-4.4.zip
RUN unzip -d /opt /tmp/sonarqube-4.4.zip
RUN mv /opt/sonarqube-4.4 /opt/sonarqube
RUN sed -i \
        -e "s#^sonar.jdbc.url.*#sonar.jdbc.url: jdbc:postgresql://127.0.0.1:5432/sonar#" \
        /opt/sonarqube/conf/sonar.properties

############################################
# Configure Supervisor
############################################

RUN echo "[program:postgresql]" >> /etc/supervisord.conf
RUN echo "command=/etc/init.d/postgresql-9.3 start" >> /etc/supervisord.conf
RUN echo "priority=10" >> /etc/supervisord.conf

RUN echo -e "\n\n[program:sonar]" >> /etc/supervisord.conf
RUN echo "command=/opt/sonarqube/bin/linux-x86-64/sonar.sh console" >> /etc/supervisord.conf
RUN echo "priority=20" >> /etc/supervisord.conf


############################################
# Start Sonar
############################################

CMD ["/usr/bin/supervisord", "-n"]

EXPOSE 9000 5432
