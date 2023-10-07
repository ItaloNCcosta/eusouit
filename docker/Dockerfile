FROM php:8.2-apache

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN apt-get update && apt-get install -y \
    zip \
		curl \
    unzip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# * * * * * * * * * setup Apache
RUN chown www-data: /var/www -R && chmod -R 777 /var/www \
	&& a2dissite 000-default && a2enmod rewrite

# * * * * * * * * * set server name
RUN echo "ServerName app.local" >> /etc/apache2/apache2.conf


WORKDIR /var/www

# * * * * * * * * * expose ports
EXPOSE 80

RUN a2enmod proxy_fcgi && a2dismod mpm_event && a2enmod mpm_prefork

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]