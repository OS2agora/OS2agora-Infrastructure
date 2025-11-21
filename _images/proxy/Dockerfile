FROM httpd:latest
COPY conf/httpd.conf /usr/local/apache2/conf/httpd.conf
COPY certificates/proxy.crt /usr/local/apache2/conf/server.crt
COPY certificates/proxy.key /usr/local/apache2/conf/server.key
RUN mkdir -p /usr/local/apache2/conf/sites/
COPY conf/sites/* /usr/local/apache2/conf/sites
