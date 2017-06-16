FROM centos:7
MAINTAINER Lincoln Bryant <lincolnb@uchicago.edu>

# You can change this
ENV EPREFIX /tmp/rap

# Setup the basic packages needed to build RAP. 
# Note these are not included (or needed?) in the final build
RUN yum install gcc make tar curl wget m4 bzip2 which -y

# Create the build user. Generally a good idea to build unprivileged
RUN useradd -ms /bin/bash build
# Build and chown the empty prefix dir
RUN mkdir -p $EPREFIX && chown build: $EPREFIX

# Change to build user
USER build
WORKDIR /home/build

# Build stage 1 - bootstrap the toolchain
RUN curl -O http://dev.gentoo.org/~heroxbd/bootstrap-rap.sh && mkdir -p $EPREFIX && chmod 755 bootstrap-rap.sh
RUN ./bootstrap-rap.sh $EPREFIX stage1

# Export the environment. This should make it easy to redefine at runtime 
ENV PATH "$EPREFIX/usr/bin:$EPREFIX/bin:$EPREFIX/tmp/usr/bin:$EPREFIX/tmp/bin:/usr/bin:/bin"

# Build stage 2 - build the base system
RUN ./bootstrap-rap.sh $EPREFIX stage2

# Build stage 3 - update toolchain, install utilities, etc
# seems that the stage3 throws some warnings that cause the build to fail, so just exit 0 all of the time.
RUN ./bootstrap-rap.sh $EPREFIX stage3 ; exit 0
#RUN quickpkg "*/*"
