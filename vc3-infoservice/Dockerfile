FROM virtualclusters/base:latest
LABEL maintainer lincolnb@uchicago.edu

COPY supervisord.conf /etc/supervisord.conf
COPY vc3-infoservice.conf /etc/vc3/vc3-infoservice.conf

CMD ["/usr/bin/supervisord","-c","/etc/supervisord.conf"]
