FROM ubuntu:16.04
MAINTAINER ganuonglachanh <ganuonglachanh>

#ARG DEBIAN_FRONTEND=noninteractive
#ENV NGINX_VERSION 1.12.1

# -----------------------------------------------------------------------------
# install nginx
# -----------------------------------------------------------------------------
RUN apt-get update -y \
	&& apt-get install -y nginx wget curl nano htop
#RUN ufw allow 'Nginx Full'
# -----------------------------------------------------------------------------
# Clean up
# -----------------------------------------------------------------------------
RUN apt-get -y clean \
  	&& rm -rf /var/lib/apt/lists/*
# -----------------------------------------------------------------------------
# asmbb
# -----------------------------------------------------------------------------
RUN cd /var/www/html \
	&& wget 'https://asm32.info/fossil/repo/asmbb/doc/trunk/install/asmbb.tar.gz' \
	&& tar -xvzf asmbb.tar.gz && mv asmbb/* ./ && rm -rf asmbb/ 
# -----------------------------------------------------------------------------
# Setting
# -----------------------------------------------------------------------------
COPY ./conf/default /etc/nginx/sites-enabled/default
#RUN systemctl restart nginx
RUN cd /var/www/html
WORKDIR /var/www/html

RUN useradd work
RUN chown -R work:work /var/www/html
RUN chown -R work:work /var/log/nginx
RUN sed -i 's/user www-data;/user root;/1' /etc/nginx/nginx.conf
#RUN nginx &
#RUN su work /var/www/html/engine &
COPY ./conf/entry.sh /home
RUN chmod +x /home/entry.sh
#RUN /home/entry.sh
# -----------------------------------------------------------------------------
# Expose our port
# -----------------------------------------------------------------------------
EXPOSE 80 443

#CMD [ "/var/www/html/engine" ]
CMD ["tail", "-f", "/dev/null"]
