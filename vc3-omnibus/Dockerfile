FROM vc3-base:latest
LABEL maintainer lincolnb@uchicago.edu
LABEL version 2017-11-27

COPY credible.conf /etc/credible/credible.conf
COPY vc3-infoservice.conf /etc/vc3/vc3-infoservice.conf
COPY vc3-master.conf /etc/vc3/vc3-master.conf
COPY tasks.conf /etc/vc3/tasks.conf
COPY vc3-client.conf /etc/vc3/vc3-client.conf
COPY supervisord.conf /etc/supervisord.conf

RUN credible -c /etc/credible/credible.conf hostcert localhost > /etc/pki/tls/certs/hostcert.pem
RUN credible -c /etc/credible/credible.conf hostkey localhost > /etc/pki/tls/private/hostkey.pem
RUN credible -c /etc/credible/credible.conf certchain > /etc/pki/ca-trust/extracted/pem/vc3-chain.cert.pem

CMD ["/usr/bin/supervisord","-c","/etc/supervisord.conf"]
