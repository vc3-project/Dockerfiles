FROM centos:centos7
LABEL maintainer lincolnb@uchicago.edu

# create unprivileged user
RUN adduser infoservice

# install dependencies
RUN yum install epel-release -y
RUN yum install python-pip git pyOpenSSL openssl -y
RUN pip install cherrypy==3.2.2


# Switch to infoservice user
USER infoservice

# Download VC3 bits
RUN mkdir -p /home/infoservice/git
RUN cd /home/infoservice/git \
    && git clone https://github.com/vc3-project/vc3-info-service.git \
    && git clone https://github.com/bnl-sdcc/pluginmanager \
    && git clone https://github.com/vc3-project/credible

# Run the info service installer
RUN cd /home/infoservice/git/pluginmanager; python setup.py install --home=~/
ENV PYTHONPATH=/home/infoservice/lib/python:$PYTHONPATH

# Run the credible installer
RUN cd /home/infoservice/git/credible; python setup.py install --home=~/

# Generate credentials
RUN ~/bin/credible -c ~/git/credible/etc/credible.conf hostcert localhost
RUN ~/bin/credible -c ~/git/credible/etc/credible.conf certchain
RUN ~/bin/credible -c ~/git/credible/etc/credible.conf usercert VC3Admin

ENV CREDROOT=/home/infoservice/var/credible/ssca/defaultca/intermediate/
ENV SRVROOT=/home/infoservice/vc3-services/etc/certs

RUN mkdir -p $SRVROOT/private && \
    cp $CREDROOT/certs/localhost.cert.pem $CREDROOT/certs/ca-chain.cert.pem $CREDROOT/certs/VC3Admin.cert.pem $SRVROOT/ && \
    cp $CREDROOT/private/localhost.keynopw.pem $CREDROOT/private/VC3Admin.keynopw.pem $SRVROOT/private/

# Run the Info Service installer
RUN cd /home/infoservice/git/vc3-info-service; python setup.py install --home=~/
# Run Info Service
CMD cd $HOME/git/vc3-info-service; vc3infoservice/infoservice.py -d --conf etc/vc3-infoservice.conf --debug
