#######################################################################
#                                                                     #
# Creates a Jenkins image with TicketMonster job configured  		  #
#                                                                     #
#######################################################################

FROM siamaksade/jenkins

MAINTAINER Siamak Sadeghianfar <ssadeghi@redhat.com>

# Generate SSH Key Pair
sudo -u jenkins ssh-keygen -t rsa -q -N "" -f /var/lib/jenkins/.ssh/id_rsa
chown -R jenkins:jenkins /var/lib/jenkins/.ssh/
chmod 755 /var/lib/jenkins/.ssh/
chmod 644 /var/lib/jenkins/.ssh/authorized_keys

# Install Plugins
RUN wget -O /var/lib/jenkins/plugins/openshift-deployer.hpi 		http://updates.jenkins-ci.org/latest/openshift-deployer.hpi
RUN wget -O /var/lib/jenkins/plugins/build-pipeline-plugin.hpi 		http://updates.jenkins-ci.org/download/plugins/build-pipeline-plugin/1.4.3/build-pipeline-plugin.hpi
RUN wget -O /var/lib/jenkins/plugins/jquery.hpi 					http://updates.jenkins-ci.org/download/plugins/jquery/1.7.2-1/jquery.hpi
RUN wget -O /var/lib/jenkins/plugins/parameterized-trigger.hpi 		http://updates.jenkins-ci.org/download/plugins/parameterized-trigger/2.25/parameterized-trigger.hpi
RUN wget -O /var/lib/jenkins/plugins/sonar.hpi 						http://updates.jenkins-ci.org/download/plugins/sonar/2.1/sonar.hpi
RUN wget -O /var/lib/jenkins/plugins/javadoc.hpi 					http://updates.jenkins-ci.org/download/plugins/javadoc/1.2/javadoc.hpi
RUN wget -O /var/lib/jenkins/plugins/delivery-pipeline-plugin.hpi 	https://updates.jenkins-ci.org/download/plugins/delivery-pipeline-plugin/0.8.6/delivery-pipeline-plugin.hpi
RUN wget -O /var/lib/jenkins/plugins/token-macro.hpi 				https://updates.jenkins-ci.org/download/plugins/token-macro/1.9/token-macro.hpi
RUN wget -O /var/lib/jenkins/plugins/jquery-ui.hpi 					https://updates.jenkins-ci.org/download/plugins/jquery-ui/1.0.2/jquery-ui.hpi

# Jenkins Settings
ADD config/jenkins-config.xml /var/lib/jenkins/config.xml

# Maven Global Settings
ADD config/maven-settings.xml /usr/share/apache-maven/conf/settings.xml

# SonarQube Settings
ADD config/sonar-settings.xml /var/lib/jenkins/hudson.plugins.sonar.SonarPublisher.xml

# Build Jobs
RUN mkdir -p /var/lib/jenkins/jobs/ticket-monster-{analysis,build,deploy-dev,func-test,release,test}

ADD config/job-analysis.xml 	/var/lib/jenkins/jobs/ticket-monster-analysis/config.xml
ADD config/job-build.xml 		/var/lib/jenkins/jobs/ticket-monster-build/config.xml
ADD config/job-deploy-dev.xml 	/var/lib/jenkins/jobs/ticket-monster-deploy-dev/config.xml
ADD config/job-func-test.xml 	/var/lib/jenkins/jobs/ticket-monster-func-test/config.xml
ADD config/job-release.xml 		/var/lib/jenkins/jobs/ticket-monster-release/config.xml
ADD config/job-test.xml 		/var/lib/jenkins/jobs/ticket-monster-test/config.xml


# Set Permissions
RUN chown -R jenkins:jenkins /var/lib/jenkins