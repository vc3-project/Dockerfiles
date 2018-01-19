FROM vc3-base:latest
LABEL maintainer lincolnb@uchicago.edu
LABEL version 2018-1-18

COPY credible.conf /etc/credible/credible.conf
COPY vc3-infoservice.conf /etc/vc3/vc3-infoservice.conf
COPY vc3-infoclient.conf /etc/vc3/vc3-infoclient.conf
COPY vc3-master.conf /etc/vc3/vc3-master.conf
COPY tasks.conf /etc/vc3/tasks.conf
COPY vc3-client.conf /etc/vc3/vc3-client.conf
COPY queues.conf /etc/autopyfactory/queues.conf
COPY vc3defaults.conf /etc/autopyfactory/vc3defaults.conf
COPY vc3authdefaults.conf /etc/autopyfactory/vc3authdefaults.conf
COPY 10-master.conf /etc/condor/config.d/10-master.conf

RUN cp /usr/etc/autopyfactory/*.conf /etc/autopyfactory

RUN mkdir -p /var/log/autopyfactory && chown autopyfactory: /var/log/autopyfactory

RUN credible -c /etc/credible/credible.conf hostcert localhost > /etc/pki/tls/certs/hostcert.pem
RUN credible -c /etc/credible/credible.conf hostkey localhost > /etc/pki/tls/private/hostkey.pem
RUN credible -c /etc/credible/credible.conf certchain > /etc/pki/ca-trust/extracted/pem/vc3-chain.cert.pem
RUN chown -R vc3: /var/credible
RUN mkdir /var/log/vc3 && chown -R vc3: /var/log/vc3

RUN mv /src/vc3-playbooks /etc/vc3/vc3-playbooks

# update the test scripts
RUN cd /src/vc3-client && git pull origin

COPY supervisord.conf /etc/supervisord.conf
CMD ["/usr/bin/supervisord","-c","/etc/supervisord.conf"]
