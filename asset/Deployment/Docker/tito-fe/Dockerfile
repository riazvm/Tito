#Created by Vincent Meoc
# Create the Tito Front End container
#Env (optional): TITODBSERVER=<FQDN/IP of MYSQL

FROM php:rc-apache
#COPY . /var/www/html/
COPY asset/Deployment/Docker/tito-fe/apache2-foreground /usr/local/bin/apache2-foreground
RUN chmod +x /usr/local/bin/apache2-foreground

RUN apt-get update
RUN apt-get install php-mysql vim libmcrypt-dev -y
RUN apt-get install git -y
RUN docker-php-ext-install mysqli pdo pdo_mysql sockets

#Deploy Tito
RUN git clone https://github.com/vmeoc/Tito /var/www/html/

RUN echo "<IfModule env_module>" >> /etc/apache2/mods-enabled/env.conf
RUN echo "     SetEnv TITODBSERVER \"TITODBSERVER\"" >> /etc/apache2/mods-enabled/env.conf
RUN echo "</IfModule>" >> /etc/apache2/mods-enabled/env.conf

ENTRYPOINT ["/usr/local/bin/apache2-foreground"]
