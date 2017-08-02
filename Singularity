#
# This will create an image with GlueX reconstruction software
# suitable for doing event reconstruction. It does NOT contain
# simulation programs (cernlib or GEANT4).
#
#  Build the image with:
#
#  docker build -f Dockerfile-recon -t hdrecon:c7 .
#
#
# This was based on some initial work by Nathan Sparks.
#

Bootstrap: docker
From: centos:7

%labels
AUTHOR "David Lawrence <davidl@jlab.org>"

%environment
GLUEX_TOP=/home/gx
export GLUEX_TOP

%runscript

source /home/gx/.hdpm/env/master.csh && /bin/tcsh


%post

yum update -y && yum install -y epel-release && yum install -y \
	curl \
	tar \
	tcsh \
	&& yum clean all \
	&& cd /home \
	&& curl -OL https://halldweb.jlab.org/dist/hdpm/gxsrc.tar.gz \
	&& tar xf gxsrc.tar.gz \
	&& rm gxsrc.tar.gz \
	&& cd gx \
	&& groupadd -r gx -g 573 \
	&& useradd -u 1000 -r -g gx -d /home/gx -s /sbin/nologin -c "Singularity image user" gx \
	&& curl -OL https://halldweb.jlab.org/dist/hdpm/hdpm-dev.linux.tar.gz \
	&& tar xf hdpm-dev.linux.tar.gz \
	&& mv hdpm-dev/bin/hdpm /usr/bin/ \
	&& rm -rf hdpm-dev hdpm-dev.linux.tar.gz \
	&& chown -R gx:gx /home/gx

su gx \
	&& cd /home/gx \
	&& /bin/bash -c "hdpm fetch -d root@binary amptools evio jana rcdb \
	&& hdpm install amptools evio jana rcdb \
	&& hdpm clean --obliterate"



