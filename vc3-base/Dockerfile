FROM centos:centos7
LABEL maintainer lincolnb@uchicago.edu
LABEL version 2018-01-18.1

# create unprivileged user
RUN adduser vc3

# install dependencies
RUN yum install epel-release centos-release-openstack-ocata -y
RUN yum install python-pip python-devel git openssl supervisor condor condor-python python-novaclient -y
RUN yum groupinstall "Development Tools" -y
RUN pip install --upgrade pip
RUN pip install pyOpenSSL cherrypy boto PyYAML requests ansible
# new error..
RUN pip install --upgrade six
RUN mkdir src

RUN pushd src && \
    git clone https://github.com/bnl-sdcc/sdcc-pluginmanager && \
    pushd sdcc-pluginmanager && \
    python setup.py bdist_rpm && \
    yum localinstall dist/*.rpm -y && \
    popd && \
    popd
RUN pushd src && \
    git clone https://github.com/vc3-project/vc3-info-service && \
    pushd vc3-info-service && \
    python setup.py bdist_rpm && \
    yum localinstall dist/*.rpm -y && \
    popd && \
    popd
RUN pushd src && \
    git clone https://github.com/vc3-project/vc3-client && \
    pushd vc3-client && \
    python setup.py bdist_rpm && \
    yum localinstall dist/*.rpm -y && \
    popd && \
    popd
RUN pushd src && \
    git clone https://github.com/vc3-project/vc3-master && \
    pushd vc3-master && \
    python setup.py bdist_rpm && \
    yum localinstall dist/*.rpm -y && \
    popd && \
    popd
RUN pushd src && \
    git clone https://github.com/vc3-project/credible && \
    pushd credible && \
    python setup.py bdist_rpm && \
    yum localinstall dist/*.rpm -y && \
    popd && \
    popd
RUN pushd src && \
    git clone https://github.com/pandawms/autopyfactory && \
    pushd autopyfactory && \
    python setup.py bdist_rpm && \
    yum localinstall dist/*.rpm -y && \
    popd && \
    popd
RUN pushd src && \
    git clone https://github.com/vc3-project/vc3-factory-plugins && \
    pushd vc3-factory-plugins && \
    python setup.py bdist_rpm && \
    yum localinstall dist/*.rpm -y && \
    popd && \
    popd 
RUN pushd src && \
    git clone https://github.com/vc3-project/vc3-playbooks && \
    popd 
