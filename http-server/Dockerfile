FROM httpd:2.4

COPY ./index.html /usr/local/apache2/htdocs/

# Ajoute une config de reverse proxy propre
RUN mkdir -p /usr/local/apache2/conf/conf.d && \
    echo '<VirtualHost *:80>' > /usr/local/apache2/conf/conf.d/proxy.conf && \
    echo '    ProxyPreserveHost On' >> /usr/local/apache2/conf/conf.d/proxy.conf && \
    echo '    ProxyPass / http://backend-spring:8080/' >> /usr/local/apache2/conf/conf.d/proxy.conf && \
    echo '    ProxyPassReverse / http://backend-spring:8080/' >> /usr/local/apache2/conf/conf.d/proxy.conf && \
    echo '</VirtualHost>' >> /usr/local/apache2/conf/conf.d/proxy.conf

# Active les modules proxy
RUN sed -i '/^#LoadModule proxy_module/s/^#//' /usr/local/apache2/conf/httpd.conf && \
    sed -i '/^#LoadModule proxy_http_module/s/^#//' /usr/local/apache2/conf/httpd.conf
