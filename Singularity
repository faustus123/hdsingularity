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
	binutils \
	blas-static \
	boost-devel \
	bzip2-devel \
	clang \
	cmake3 \
	curl \
	expat-devel \
	fftw-devel \
	file \
	gcc \
	gcc-c++ \
	gcc-gfortran \
	imake patch \
	lapack-devel \
	lapack-static \
	libXext-devel \
	libXft-devel \
	libXi-devel \
	libXmu-devel \
	libXpm-devel \
	lsof \
	make \
	man \
	openmotif-devel \
	python-devel \
	scons \
	sqlite-devel \
	subversion \
	tar \
	tcsh \
	xerces-c-devel \
	blas-devel \
	bzip2 \
	git \
	libX11-devel \
	mesa-libGLU-devel \
	mysql-devel \
	which \
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
	&& cd /home/gx \
	&& export GLUEX_TOP=/home/gx \
	&& /bin/bash -c "hdpm fetch -d root@binary amptools evio jana rcdb \
	&& hdpm install amptools evio jana rcdb \
	&& hdpm clean --obliterate" \
	&& chown -R gx:gx /home/gx



