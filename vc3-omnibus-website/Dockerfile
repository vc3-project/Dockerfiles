FROM vc3-base:latest
LABEL maintainer lincolnb@uchicago.edu
LABEL version 2017-11-29

COPY credible.conf /etc/credible/credible.conf
COPY vc3-infoservice.conf /etc/vc3/vc3-infoservice.conf
COPY vc3-master.conf /etc/vc3/vc3-master.conf
COPY tasks.conf /etc/vc3/tasks.conf
COPY vc3-client.conf /etc/vc3/vc3-client.conf
COPY supervisord.conf /etc/supervisord.conf

RUN credible -c /etc/credible/credible.conf hostcert localhost > /etc/pki/tls/certs/hostcert.pem
RUN credible -c /etc/credible/credible.conf hostkey localhost > /etc/pki/tls/private/hostkey.pem
RUN credible -c /etc/credible/credible.conf certchain > /etc/pki/ca-trust/extracted/pem/vc3-chain.cert.pem

##########
# Website
##########
RUN yum install nginx uwsgi uwsgi-plugin-python -y
RUN mkdir -p /srv/www
RUN git clone https://github.com/vc3-project/vc3-website-python /srv/www/vc3-web-env
RUN cd /srv/www/vc3-web-env; pip install -r requirements.txt

COPY vc3.ini /etc/uwsgi.d/vc3.ini
COPY uwsgi_params /etc/nginx/uwsgi_params
COPY nginx.conf /etc/nginx/nginx.conf

CMD ["/usr/bin/supervisord","-c","/etc/supervisord.conf"]
