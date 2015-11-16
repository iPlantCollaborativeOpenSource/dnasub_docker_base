# docker build --rm --pull=true -t iplantc/dnasub_core .

FROM centos:centos5
MAINTAINER Matthew Vaughn <vaughn@tacc.utexas.edu>

ENV _APP DNALC Lonestar4 runtime base
ENV _AUTHOR Matthew Vaughn
ENV _LICENSE MIT
ENV _VERSION 0.0.1
ENV AGAVE_USERNAME ""
ENV AGAVE_PASSWORD ""

# Set up /opt/bin and permantly set PATH
RUN mkdir -p /opt/bin
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/bin
WORKDIR /home

# Basics
RUN yum -y install curl wget which bzip2 java-1.7.0-openjdk.x86_64 && yum clean all
# Ugh. X11 is needed for R and other stuff
RUN yum -y groupinstall "X Window System" "X Software Development" && yum clean all

# Install git as per https://gist.github.com/eddarmitage/2001099
RUN wget --no-check-certificate http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el5.rf.i386.rpm
RUN rpm --import http://apt.sw.be/RPM-GPG-KEY.dag.txt && rpm -K rpmforge-release-0.5.2-2.el5.rf.i386.rpm && rpm -i rpmforge-release-0.5.2-2.el5.rf.i386.rpm && rm rpmforge-release-0.5.2-2.el5.rf.i386.rpm
RUN yum -y install git-gui && yum clean all

# Install foundation-cli
RUN git clone https://bitbucket.org/taccaci/foundation-cli.git /opt/bin/agave-cli && chmod -R a+r /opt/bin/agave-cli/bin
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/bin:/opt/bin/agave-cli/bin
# Automatically config root user for iplantc.org tenant
RUN /opt/bin/agave-cli/bin/tenants-init --tenant 1
