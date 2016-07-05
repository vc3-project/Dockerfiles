FROM centos:6
MAINTAINER Lincoln Bryant <lincolnb@uchicago.edu>

ENV prefix /tmp/rap

# Install the minimum dependencies to build
RUN yum install gcc make tar curl wget m4 bzip2 which -y

RUN useradd -ms /bin/bash build
USER build
WORKDIR /home/build
RUN curl -O http://dev.gentoo.org/~heroxbd/bootstrap-rap.sh && mkdir ${prefix} && chmod 755 bootstrap-rap.sh

# terrible hack b/c of portage not finding our bootstrapped python
RUN ./bootstrap-rap.sh ${prefix} stage1; exit 0
USER root
WORKDIR /root
RUN rm -f /usr/bin/python && ln -s ${prefix}/tmp/usr/bin/python /usr/bin/python

# continue the stage1 build
USER build
WORKDIR /home/build
RUN ./bootstrap-rap.sh ${prefix} stage1

RUN export EPREFIX=${prefix} && export PATH="$EPREFIX/usr/bin:$EPREFIX/bin:$EPREFIX/tmp/usr/bin:$EPREFIX/tmp/bin:/usr/bin:/bin" && ./bootstrap-rap.sh ${prefix} stage2
RUN export EPREFIX=${prefix} && export PATH="$EPREFIX/usr/bin:$EPREFIX/bin:$EPREFIX/tmp/usr/bin:$EPREFIX/tmp/bin:/usr/bin:/bin" && ./bootstrap-rap.sh ${prefix} stage3

# make binaries
RUN export EPREFIX=${prefix} && export PATH="$EPREFIX/usr/bin:$EPREFIX/bin:$EPREFIX/tmp/usr/bin:$EPREFIX/tmp/bin:/usr/bin:/bin" && emerge -uDN @world --buildpkg
