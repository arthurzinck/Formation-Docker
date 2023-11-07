FROM ubuntu:jammy
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \ 
    apt install -y apache2 \
    apache2-utils php \
    php-mysql libapache2-mod-php
EXPOSE 80
CMD ["apachectl", "-D", "FOREGROUND"]
