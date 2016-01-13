FROM alpine:3.1

MAINTAINER John Allen <john.allen@connexiolabs.com>

ENV NGINX_VERSION nginx-1.7.11

RUN apk --update add openssl-dev pcre-dev zlib-dev wget build-base && \
    mkdir -p /tmp/src && \
    cd /tmp/src && \
    wget http://nginx.org/download/${NGINX_VERSION}.tar.gz && \
    tar -zxvf ${NGINX_VERSION}.tar.gz && \
    cd /tmp/src/${NGINX_VERSION} && \
    ./configure \
        --with-http_ssl_module \
        --with-http_gzip_static_module \
        --prefix=/etc/nginx \
        --http-log-path=/var/log/nginx/access.log \
        --error-log-path=/var/log/nginx/error.log \
        --sbin-path=/usr/local/sbin/nginx && \
    make && \
    make install && \
    apk del build-base && \
    rm -rf /tmp/src && \
    rm -rf /var/cache/apk/*

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

# Define mountable directories.
VOLUME ["/var/log/nginx"]

# Remove the default Nginx configuration file
#RUN rm -v /etc/nginx/nginx.conf

# Copy a configuration file from the current directory
ADD nginx.conf /etc/nginx/

# delete default, copy over local webpage from local folder to root of server
RUN rm -v /etc/nginx/html/index.html
ADD html/index.html /etc/nginx/html


# Define working directory.
WORKDIR /etc/nginx

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
