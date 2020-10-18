FROM debian:latest

USER root

RUN apt update && apt-get upgrade -y && apt-get install -y \
	apache2 \
	php \
	php-xml \
	php-mbstring \
	php-curl \
	php-zip \
	php-bcmath \
	php-mysql \
	mariadb-server \
	wget
RUN rm /var/www/html/index.html
RUN wget https://files.froxlor.org/releases/froxlor-latest.tar.gz && cp froxlor-latest.tar.gz /var/www/html/. && cd /var/www/html && tar -xzf froxlor-latest.tar.gz && mv froxlor/* .

ADD froxlor-config-20201016.json /root/.
RUN chown www-data:www-data /var/www/html -R
ADD userdata.inc.php /var/www/html/lib/userdata.inc.php
RUN php /var/www/html/install/scripts/config-services.php --apply=/root/froxlor-config-20201016.json
CMD /usr/sbin/apache2ctl -D FOREGROUND