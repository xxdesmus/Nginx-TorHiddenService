FROM gliderlabs/alpine

MAINTAINER Jake 

RUN apk-install ca-certificates nginx

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

# Define mountable directories.
VOLUME ["/var/log/nginx"]

# Copy a configuration file from the current directory
ADD nginx.conf /etc/nginx/

# delete default, copy over local webpage from local folder to root of server
RUN rm -v /usr/share/nginx/html/index.html
ADD html/* /usr/share/nginx/html/

# Define working directory.
WORKDIR /etc/nginx

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
