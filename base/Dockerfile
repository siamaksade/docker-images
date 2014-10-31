#######################################################################
#                                                                     #
# Creates a base CentOS image							  			  #
#                                                                     #
#######################################################################

# Use the centos base image
FROM centos:centos6

MAINTAINER Siamak Sadeghianfar <ssadeghi@redhat.com>

USER root
# Update the system
RUN yum -y update; yum clean all

##########################################################
# Install Java JDK and other useful cmdline utilities
##########################################################
RUN yum -y install java-1.7.0-openjdk-devel which unzip sudo openssh-clients iputils iproute httpd-tools wget tar; yum clean all
ENV JAVA_HOME /usr/lib/jvm/jre

############################################
# Install Supervisor
############################################
RUN yum -y localinstall http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm 
RUN yum -y install supervisor

CMD true

